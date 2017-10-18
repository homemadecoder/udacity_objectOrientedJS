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
-parameter of a method indication
