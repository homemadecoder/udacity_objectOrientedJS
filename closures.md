# Closures
Every function should have access to all the variables from all the scopes that surround it.

### Closure
- any function that somehow remains available after those after those outer scopes have returned
- if you store an array in a global variable, calls to that push should have a lasting effect on it that persists even after new saga has finished running
- the context for a function will always be created as a child of the context that it was defined within
- a new context always gets created in the same context as its function was defined within