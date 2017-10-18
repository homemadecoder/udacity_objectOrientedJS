# This

Every object-oriented language has a way to dynamically refer to the current objet. In JS, it doesn't alway return the object you're expecting it to.

### Parameter this
- behaves almost exactly like a normal parameter, with a couple of exceptions

**Parameters** - those words that we see between parenthesis in a function definition

##### Parameter this vs normal parameter
- you don't get to pick the name for the parameter this
- you go about binding values to the parameter this a bit differently from how you bind values to other paramters

### This
- an identifier that gets a value bound to it, much like a variable
- but instead of identifying the values explicitly in your code, this gets bound to the correct objet automatically
- the rules for how the interpreter determins what the correct binding is, resemble the rules for positional function parameters
- the differences between positional function parameters and the keyword this are designed to support your intuition about which object should be focal when you're invoking a method or a constructor

##### What 'this' is not bound to

```
var fn = function(a,b){ //function definition
  log(this);
};
```
1. the funciton object this appears within
- interpreter will create a function object in memory

2. a new instance of the function this appears within
- an instance of that function is created and the keyword this refers to it

3. an object happens to have that function as a property 
- in order for the keyword this to mean anything, it must be in a function that is contained within some other object as a property
```
var ob2 = {method: fn};
```

4. the object created by the literal this appears within 
```
var obj = {
  fn : function(a,b){ 
  log(this);
  }
};
```

##### What 'this' is bound to
```
obj.fn(3,4);
```
- when you notice a dot to the left of a function invocation, meaning it was looked up as a property of an object, you can look to the left of that dot and see what object it was looked up upon
- the object that a function is looked up upon when it's being invoked, that object is what the keyword **this** will be bound to
- call time dot and the object we find to the left of it 


### This 
- in JS, the keyword this behaves like a parameter in most of the important ways
- the intuitions that you've built up around how to pass values into a function and how they'll get bound to the arguments being passed in at call time, all those same intuitions will hold true for the parameter this
- parameter of a method indication
- when you don't have a dot to help you pass a specific binding for the keyword this, JavaScript binds this by default to the global object
- similar to the fact that JavaScript binds undefined to positional parameters when we call the function without enough inputs
- the default object of global would be bound to this whenever we don't have a dot

```
var fn = function(one, two){
  log(this, one, two);
};
var r = {}, g = {}, b = {};
r.method = fn;
r.method(g,b);
fn(g,b);
```

- the dot is the mechanism by which we pass in a binding for the keyword this
- without a dot, you could expect that some default value to get bound to the parameter this
- has the effect of assigning global as the default binding for this

### .call
- besides the left of the dot rule, there's another way to specify the value that you'd like the parameter this to get bound to
-  override the default binding to global and override the left of the dot rule
- pass any value to get it bound to the keyword this
```
fn.call(r,g,b);
```
- when using .call, we pass in one extra value at the beginning of the argument list and that value will be bound to the parameter this
```
r.method.call(y,g,b);
```
- the use of .call overrides the method access rules, so this will get bound to the y object

### setTimeout(fn, 1000)
- source code/documentation
- setTimeout has no way of knowing what values you wanted passed to your function
- it will be forced to invoke it with no parameters at all
- when no values are passed to a function invocation, the parameters get bound to the values undefined
```
var setTimeout = function(cb, ms){
  waitSomehow(ms);
  cb();
};
```
- find call time, look for a dot and look to the left of the dot
- look at the last line of the code in setTimeout where cb gets invoked
- if there's no dot, the rule about default case is being exercised
- only the moment of call time influences how the parameter this will get bound to
- free function invocation vs method invocation with a dot

The problem of losing parameter bindings is pretty widespread since any function like setTimeout that takes another function as a callback may actually call that function differently than you expected. Call back functions are inherently designed so that they will be invoked by the system you pass them to. Thus, you generally have very little control over what the bindings will be for the parameter of the functions that you passed in.
- be careful about all the parameter bindings, including the parameter this, whenever you pass a function as an input to another function.
- despite the fact that you see an object on the left of the dot when you pass the function in, this object will not be passed along as the binding for the parameter this when the system you passed it to eventually calls your callback function
- one way to pass the callback without complicating the parameter binding situation is to pass a different function, one that doesn't receive any parameters at all, including this
```
setTimeout(function() {
  r.method;
  }, 1000);
```
- then make room in the body of that function for your custom code
- inside that area, reference your method and then you can do the invocation yourself, passing along whichever bindings you want for the parameter this

```
log(one); //error, not accessible from the global scope
log(this); //default binding to the global object
```
- language has been setup so that you can refer to this from the global scope
- this behavior was removed in the modern specifications of the language

### new r.method(g,b)
- pattern built to support mechanisms on psuedo-classical classes
```
new r.method(g,b);
```
- calling function with the key word new before it
- this has an effect on how the keyword this receives it binding
- positional parameters are unaffected by keyword new, they get passed along in exactly the same way as they always are
- the keyword this will be bound to an entirely new object that gets created automatically in the background as a result of the keyword new having appeared
- in support of certain object-oriented paradigms, another object will be generated every time you make a call to that function with the keyword new in front of it

The keyword this makes it possible for it to build just one function object and use that as a method on a bunch of other objects.

Every time we call the method, it'll have access to whatever object it's being called on. This can be really useful for conserving memory, and it's only possible because we have access to the parameter this.