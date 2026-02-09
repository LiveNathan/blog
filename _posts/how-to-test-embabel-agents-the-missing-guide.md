What's the hardest thing about writing tests?

The setup.

No one wants to write tests because no one wants to stop to think about the setup. What inputs do we need? How do we get them? What outputs do we expect?

Luckily, Embabel provides a fake OperationContext out of the box. Unluckily, that won't get you very far. The fake that Embabel provides will help you with a single builder test and thats it. That will help you get started and make sure that you wrote the builder correctly, but it won't help you with the really important stuff – actually testing the agent.

This is the missing guide.

## The boring stuff

Let's get the boring stuff out of the way.  we'll use the fake OperationContext to lock the builder values in place.

Let's build a simple agent to classify user input as a query or a command. We love TDD so we'll start with a failing test.

// test

We expect the test to fail because it won't compile because there's no production code, yet.

// prod

Now the test passes as expected.

Ok, now that we've gotten the boring stuff out of the way, let's do the fun stuff.

## The fun stuff

What do we expect the agent to do?

At a minimum it should return the expected output object. Beyond that the output object should contain the expected content. Let's see if we can come up with an intial list of expectations to drive the design.
- [ ] givenValidInput_whenClassified_thenReturnsExpectedObject
- [ ] givenThisUserMessage_whenClassified_thenReturnsExpectedContent
- [ ] givenThisUserMessage_whenClassified_thenReturnsExpectedOutput

// first test

This test will pass because it's so simple. Should we make it more complex or change the test to first convince ourselves that it fails for the expected reason?

## Conclusion