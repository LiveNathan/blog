---
layout: post
title: "Migrating from Railway to Coolify: Java Spring Boot with PostgreSQL and Redis"
date: 2025-03-22 09:00:00 -0000
categories: [ devops, java, spring-boot, postgresql, redis, migration, subaligner ]
---

If you've been following along with my journey, you might know that [SubAligner](https://www.subaligner.com/) is the
reason I learned Java. Today I want to share how I recently migrated this application from Railway to Coolify, why I did
it, and how you can avoid the mistakes I made along the way.

## Contents

- [The Origin Story](#the-origin-story)
- [Why I Left Railway](#why-i-left-railway)
- [Preparing for Migration](#preparing-for-migration)
- [The Migration Plan](#the-migration-plan)
- [What Actually Happened](#what-actually-happened)
- [Lessons Learned](#lessons-learned)

## The Origin Story

SubAligner wasn't just any project for me—it was the catalyst that transformed me from a live sound engineer into a
software developer. During the pandemic, I wanted to build an app to help live sound engineers with subwoofer alignment
using
the "[relative absolute method](https://www.merlijnvanveen.nl/en/nl/studiezaal/166-subwoofer-alignment-the-foolproof-relative-absolute-method)" (
one of the few
things [loudspeaker manufacturers seem to agree on](https://www.sounddesignlive.com/sub-alignment-l-acoustics-db-nexo-coda-rcf-funktion-one-db-technologies/)).

I initially tried working with a cofounder, but that partnership quickly dissolved. Without money or traction, why would
someone work for free to build *my* dream? I hate waiting and asking for permission and I have not funding so I decided
to become my own technical cofounder.

My journey took me from Excel spreadsheets to MATLAB (which I later learned is terrible for sharing unless everyone has
MATLAB), and I eventually started exploring Python. But my life changed dramatically after a conversation with a
university theater sound engineer leaving to become a software developer through a coding bootcamp.

I had no idea you could change careers in just a few months of intense study! After speaking with a bootcamp founder
about my application goals, he convinced me to learn Java—which I honestly thought was obsolete. Five months and $9,000
later, I finished the bootcamp and faced my first major challenge: deployment.

After struggling for days with Google Cloud and AWS deployments (despite extensive bootcamp training on AWS), I
discovered Railway. The concept of platform-as-a-service blew my mind—linking to a GitHub repo was essentially all I
needed. What had taken a week of frustration elsewhere took just 30 minutes on Railway.

## Why I Left Railway

Railway was perfect when I started — a simple setup and initially very affordable at
just $5/month. I eventually upgraded to $20/month for better performance, but as my application grew, so did the costs.
After six months, I was paying $80/month.

That would be fine if SubAligner were generating thousands in monthly revenue, but after a couple of years of
development, I plateaued at around $800 MRR. When your hosting costs consume 10% of your gross revenue, it's time to
reconsider your options.

Thanks to [Ted M Young](https://ted.dev/), I discovered Coolify as a viable alternative. For
approximately $10/month on Hetzner plus $5/month for Coolify's paid plan (though Coolify itself is free and
self-hosted), I could drastically reduce my infrastructure costs while gaining additional benefits.

I was initially nervous about making the switch. My DevOps skills were (and still are) pretty weak—I only know the bare
minimum for basic deployments. But with careful planning and the help from Claude, I managed to execute a successful
migration with minimal downtime.

## Preparing for Migration

The key to this successful migration was preparation. I worked on developing a comprehensive plan, spent a day debugging
that plan, rehearsed for an hour to find any remaining issues, and then executed the actual migration in about 30
minutes.

Here's what my preparation process looked like:

1. **Research and Comparison**: I thoroughly researched Coolify's capabilities and limitations, making sure it could
   handle everything my Spring Boot application needed.

2. **Environment Setup**: Before touching the live application, I created PostgreSQL and Redis instances in Coolify,
   transferred environment variables, and created the appropriate application configuration. (eg.
   application-coolify.properties)

3. **Test Migrations**: I performed multiple test migrations using database dumps from production to work out any kinks
   in the process. I struggled for a while at the beginning because the websocket connection would time out on Coolify's
   embedded terminal. ssh into the server fixed that. Thanks so much to [Cinzya](https://cinzya.gg/) on the Coolify
   Discord for the support.

4. **Simplified Dependencies**: One of the biggest challenges was Spring Session with Redis. My implementation was
   somewhat flaky and needed updating, so I simplified the SessionService to update only the current session and removed
   complex Redis session repository dependencies.

5. **Runbook Creation**: I created a detailed runbook with every command I'd need, complete with expected outputs and
   troubleshooting steps.

## The Migration Plan

The final migration plan was divided into three phases:

### Pre-Migration (1–2 days before)

- Draft maintenance window notifications
- Perform a full test migration with recent data
- Time each step to estimate downtime
- Verify third-party integrations (Stripe, Google OAuth, email)  (ooof, just realizing that I never actually did this
  until AFTER the DNS update)
- Test the staging environment with a subset of data

### Migration Day

1. **Initiate Maintenance Window**
    - Set Railway database to read-only mode
    - Post maintenance notifications

2. **Create Final Railway Backup**
   ```bash
   # Create compressed backup (-Fc)
   railway run pg_dump -Fc -U postgres -d railway -n subaligner_java > final_migration_backup.dump
   
   # Make a backup of the backup
   cp final_migration_backup.dump final_migration_backup_copy.dump
   ```

3. **Transfer and Import Database**
   ```bash
   # Transfer to Coolify server
   scp -i ~/.ssh/my_key final_migration_backup.dump root@server_ip:~/db_migration/
   
   # On the server, copy to PostgreSQL container
   docker cp ~/db_migration/final_migration_backup.dump postgres_container_id:/tmp/
   
   # In the container - reset schema
   psql -U $POSTGRES_USER -d $POSTGRES_DB
   DROP SCHEMA subaligner_java CASCADE;
   CREATE SCHEMA subaligner_java;
   
   # Import the dump
   pg_restore -d $POSTGRES_DB -U $POSTGRES_USER -n subaligner_java --no-owner /tmp/final_migration_backup.dump
   ```

4. **Verification**
   ```sql
   -- Verify record counts match
   SELECT COUNT(*) FROM subaligner_java.users;
   SELECT COUNT(*) FROM subaligner_java.payments;
   SELECT COUNT(*) FROM subaligner_java.pre_alignments;
   SELECT COUNT(*) FROM subaligner_java.user_alignments;
   ```

5. **DNS Configuration**
    - Update DNS records to point to the Coolify instance
    - Verify DNS propagation

6. **Service Activation and Testing**
    - Verify application startup
    - Test core functionality (login, alignments, payments)
    - Monitor logs for errors

7. **End Maintenance Window**
    - Remove maintenance notifications
    - Keep Railway running in read-only mode for 24-48 hours as a fallback

### Post-Migration

- Monitor for 24 hours
- Verify all subscriptions remain intact
- Take final Railway backup
- Decommission Railway after 48 hours of successful operation

## What Actually Happened

The actual migration went surprisingly smoothly, taking only about 30 minutes from start to finish. The biggest
challenge was fixing the Spring Session and Redis integration.

One important lesson in working with AI is that it will often lead you down increasingly complex paths when trying to
solve a problem. The best approach is to stop, reassess, and simplify. For me, that meant reading the Spring Session
documentation and implementing a much simpler solution than initially proposed.

Here's what I actually did to fix the session management:

1. First, I tried a complex workaround with a mock session repository, but that led to more problems

2. Eventually, I simplified by:
    - Updating the Spring Boot dependencies to the latest version
    - Adding just the essential Redis configuration
    - Using Spring's built-in session management

```properties
# Simplified Redis configuration
spring.data.redis.host=${REDIS_HOST}
spring.data.redis.port=${REDIS_PORT}
spring.data.redis.password=${REDIS_PASSWORD}
```

The database migration required attention to PostgreSQL version differences (Railway was on 15.4, Coolify on 16.8). I
had to ensure I was using compatible pg_dump/pg_restore tools:

```bash
# Check version (should be 16.x or higher)
pg_dump --version

# Install PostgreSQL 16 on macOS if needed
brew install postgresql@16
```

I also ran into an issue with large object (LOB) references that was fixed by setting avatar fields to NULL:

```sql
UPDATE subaligner_java.users
SET avatar = NULL
WHERE avatar IS NOT NULL;
```

It's been three days since the migration (I did it on Monday, and today is Thursday), and I've seen no bugs myself nor
heard any complaints from users. As planned, I've canceled my Railway subscription, which means I'll be about $65 richer
every month going forward.

## Lessons Learned

1. **Platform Risk is Everywhere**: When I started with no-code builders like Bubble.io and Unicorn Platform, I learned
   about platform lock-in the hard way. While containers make migration easier, there's always some friction when
   changing platforms.

2. **Cost Grows with Usage**: What starts as a $5/month service can quickly grow to $80/month as your application
   scales. Always factor potential growth into your platform decisions. When I started on bubble.io it
   was $15/month. Now it's $39/month.

3. **Simplify Before Migrating**: The best preparation for migration is simplification. Remove unnecessary dependencies
   and complex configurations before migrating.

4. **Version Compatibility Matters**: PostgreSQL version differences caused subtle issues. Always verify tool and
   database version compatibility.

5. **Test, Test, Test**: Multiple rehearsals prevented what could have been hours of downtime. Each rehearsal uncovered
   issues I hadn't expected.

6. **Simple Solutions Win**: When faced with complex problems (like session management), stepping back and implementing
   a simpler solution is often better than attempting complex workarounds.

7. **Document Everything**: My detailed migration plan made execution much smoother and will be invaluable if I need to
   migrate again in the future.

The migration from Railway to Coolify wasn't just about saving money; it was about gaining control over my
infrastructure without drowning in complexity. For small-to-medium projects like SubAligner, finding this balance is
crucial for sustainability.

Have you migrated between hosting platforms? I'd love to hear about your experiences and any tips you might have for
others considering similar moves.