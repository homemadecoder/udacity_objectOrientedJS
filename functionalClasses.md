# Functional Classes

## Class
- powerful fowm of functions that can be sued to manufacture fleets of similar objects
- a construct that is capable of building a fleet of similar objects that all conform to roughtly the same interface
- the notion of a category of things that you'd like to build and all of the entailed code that supports that category.


### Decorator code vs Classes
```
var carlike = function(obj, loc){
  obj.loc = loc;
  obj.move = function(){
    obj.loc++;
  };
};

var amy = carlike({}, 1);
amy.move();
var ben = carlike({}, 9);
ben.move();
```

- a class builds the object that it's going to augment
- a decorator accepts the object it's going to augment as an input

```
var Car = function(loc){
  var obj = {loc: loc};
  obj.move = function(){
    obj.loc++;
  };
  return obj;
};

var amy = Car(1);
amy.move();
var ben = Car(9);
ben.move;
```

- it's conventional to name your class with a capitalized noun, like a proper noun for a category of things

### Constructor functions
- functions that produce fleets of similar objects
- construct objects that will qualify as members of the class
- the function that you use to produce a new instance of that class

### Instances of the class
- the objects that get returned from the constructor funciton invocations

### Instantiating (operation)
- when we call a constructor function in order to create an instance

### Reducing duplicity
```
var move = function(){
  this.loc++;
};
```
- this replaces obj because this function is being called as a method on objects created with Car
- the parameter this is going to treat the object found on the left of the data call time as a function input and therefore, it will provide a name that we can use to refer to that object

### Functional shared patterns
- functional class pattern
```
var Car = function(loc){
  var obj = {loc: loc};
  obj.on - on;
  obj.off = off;
  obj.move = move;
  return obj;
};

var move = function(){
  this.loc++;
};

var on = function(){};
var on = function(){};
```

### Adding methods to classes, property access
```
var Car = function(loc){
  var obj = {loc: loc};
  extend(obj, methods);
  return obj;
};
Car.methods = {
  move: function(){
    this.loc++;
  };
};
```

Functions are just specialized objects.
They have the power of being invoked.
They are also capable of storing properties just like any other object.

There's no intercation between the properties of a function and what you expect to happen when you invoke that function.

The invocation of the function only makes the lines inside the body execute. Invoking a function has no interaction with any of the properties of that function. 

- using property access with the purpose of decluttering the methods object out of the glocal scope

# Conclusion
Functions are extremely important in JavaScript and they create the core of JavaScript classes. 

A JavaScript class is just a function that's capable of creating many similar objects. 

Anytime a function produces objects that all conform to roughly the same interface of methods and properties that would be called a class. But it is important to know that this definition draws some controversy, because there are good arguments out there, that classes really shouldn't be boiled down so simply.
