# Scope

### Lexical Scope
- region in source code where you can refer to a variable by name without getting access errors
- a new lexical scope is created every time you type out a function definition
- the two curly braces around the function's body enclosed the area of the code where different access rules will apply
- once you've made a new lexical scope by defining a function, it has a few more limits than the lexical scope around it
- you can still access variables from the broader lexical scope containing that interlexical scope, and you can access variables that get defined inside that inner scope
- variables you find in the inner scope cannot be referred to from outside that scope(will result in an error)

##### Global Scope
- can be accessed anywhere in the program
- can be shared across different files as a way for any part of the program to interact with any other part
- every other line of code can reference it
- after defining a variable in a lexical scope, you may make reference to that variable from anywhere else in that lexical scope

##### Scoping Limitations
- JS allows you to assign to variables you've never even declared before
- variables that you're assigning to for the first time will be added automatically to the global scope, not to whatever scope you did the assignment in (bad practice)
- Scoping limitations allow us to think about less of our program all at once

### Execution Contexts
- when a program runs, it builds up storage systems for holding the variables and their values
- these in-memory scope structures are called execution contexts
- they are built as the code runs, not as it's typed
- the rules govern which variables a program has access to at different points during the execution
- as the program runs, it will be building up internal data stores for keeping track of all the variables that are available to different function objects
- execution context data store - in-memory global context to hold all of the global variables
- as the first line of code runs, the interpreter builds up a new key value mapping inside of the execution context, in order to keep track of the value that is bound to the name
- new context = interpreter's current context, lookup focus
- running a function a second time will create totally new execution context instead of referencing the original context
- this accommodates for storage of different bindings

Although the second function was created by the same lines of code that created the first one, the two would fail a triple equals test that compared them.

Creating two equivalent looking functions, but that have different identities, is exactly like what happens when you see an array literal appearing within a function definition. Calling that function twice creates two different array objects. 
```
var makeArray = function(){
return [];
};
```