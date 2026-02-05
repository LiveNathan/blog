What's the hardest thing about writing tests?

The setup.

No one wants to write tests because no one wants to stop to think about the setup. What inputs do we need? How do we get them? What outputs do we expect?

Luckily, Embabel provides a fake OperationContext out of the box. Unluckily, that won't get you very far. The fake that Embabel provides will help you with a single builder test and thats it. That will help you get started and make sure that you wrote the builder correctly, but it won't help you with the really important stuff – actually testing the agent.

This is the missing guide.

## The boring stuff

Let's get the boring stuff out of the way.  we'll use the fake OperationContext to lock the builder values in place.

Let's build a simple agent to classify user input as a query or a command. We love TDD so we'll start with a failing test.
