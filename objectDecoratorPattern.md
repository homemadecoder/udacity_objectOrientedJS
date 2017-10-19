# Object Decorator Pattern

When writing software, code reuse is the practice of writing generalized code that can be relied upon to address a variety of similar goals.

Whenever you notice that two parts of your code have similarities, there's an opportunity to factor our the similar aspects of it into some reusable library code.

### Code Reuse
- the practice of writing generalized code that can be relied upon to address a variety of different goals
```
var amy = {loc:1};
//global variable, in-memory value/object
amy.loc++;
var ben = {loc:9};
ben.loc++;
```

library
- generalized code 
```
var move = function(car){
  car.loc++;
};
var amy = {loc:1};
move(amy);
var ben = {loc:9};
move(ben);
```

### Benefits of refactoriing code
- DRY code
- improve experience of refactoring code down the line
```
var move = function(car){
  car.loc = cosine(car.loc+10/2)
};
```
### Decorator function
```
var carlike = function(obj, loc){
  obj.loc = loc;
  return obj;
};
```
When a function takes in an object as it's input and then augments that object with some properties of functionality, it's called as a decorator.

It's common to use adjectives as the names for decorator functions: carlike.

### Adding Methods to Constructors
```
var carlike = function(obj, loc){
  obj.loc = loc;
  obj.move = move;
  return obj;
};

var move = function(){
  this.loc++;
};
```
- this parameter is automatically bound to the object on the left of the call time dot

# Recap of the 'this' parameter
```
var ob1 = {};
var ob2 = {};
ob1.example = function(arg1){
  log(this, arg1);
};
ob1.example(ob2);
```
- this is like an input parameter, bound to the value of the left of the dot at call time
- call time parens = binding for the first positional parameter
- call time dot = binding for the parameter this 

### Refactoring to consolidate code
```
var carlike = function(obj, loc){
  obj.loc = loc;
  obj.move = function(){
    this.loc++;
  };
  return obj;
};
```

### Predicting Strict Comparison of Objects
```
var makeAnObject = function(){
  return {example: 'property'};
};
var ob1 = makeAnObject();
var ob2 = makeAnObject();
log(ob1 === ob2); //false
```
This simple maker function builds and returns a brand new object.
Even though the exact line of code was used to generate the two different objects, they are themselves different objects.
Changes you make to one object will not have any effect on the other object because they have different identities(like two real world identical twins, look the same but has its own identity).

### Strict Comparison of Returned functions
```
var makeAnObject = function(){
  return function(){};
};
var ob1 = makeAnObject();
var ob2 = makeAnObject();
log(ob1 === ob2); //false
```

### Refactoring the .move() method
- every time the interpreter visits the middle line of the carlike decorator, a new function will be generated as the car's .move method
- advantage to putting the .move method inside the body of the carlike decorator function:
Now that the .move function is being created every time, each one has access to a unique closure scope created when we invoke the carlike function, thus, we don't need to rely on the keyword this anymore
```
var carlike = function(obj, loc){
  obj.loc = loc;
  obj.move = function(){
    obj.loc++;
  };
  return obj;
};
```
Instead of referring to the parameter this, which gets bound to a new value every time move is invoked, we could instead refer to the closure variable obj.
Each time we call the carlike function, a new closure scope is created and therefor the obj variable will always refer to exactly one car object

# Conclusion
Generally, you would use the decorator pattern to add some functionality to an object that already had some functionality in it at that point