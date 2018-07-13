# Why Mutations have to run Synchronously

Mutations face one big issue - they always have to by synchronous. We must not run any asynchronous taks (e.g. set timeout or reach a server) in such a mutation. Otherwise the main benefit of the mutation, namely having easy to track adjustment of our `state`, so knowing when the `state` gets changed, gets lost, because if that happens asynchronously we can't track which `mutation` was responsible for which `change`.

But how do we then combine both? => 010_How Actions Improve Mutations