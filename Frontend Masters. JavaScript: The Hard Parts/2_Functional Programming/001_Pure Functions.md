# Pure Functions

Functional programming core features

1. Pure `functions` (no side effects). When you write a `function`, its only concequense is determined by returned `value`. But it's not changing anything in the global context.

The definition of a pure function is:

- The `function` always returns the same result if the same `arguments` are passed in. It does not depend on any state, or data, change during a program’s execution. It must only depend on its input `arguments`.
- The `function` does not produce any observable side effects such as network requests, `input` and `output` devices, or data mutation.

**What Are Observable Side Effects?**

An observable side effect is any interaction with the outside world from within a `function`. That could be anything from changing a `variable` that exists outside the `function`, to calling another `method` from within a `function`.

Note: If a `pure function` calls a `pure function` this isn’t a side effect and the calling `function` is still pure.

Side effects include, but are not limited to:

- Making a HTTP request
- Mutating data
- Printing to a screen or console
- DOM Query/Manipulation
- Math.random()
- Getting the current time



2. `Higher order functions` - highly valuable tool & often part of the Codesmith interview

