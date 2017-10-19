# Prototype Chains
Prototype chains are a mechanism for making objects that resemble other objects. When you want two objects to have all the same properties, either to save memory or to avoid code duplication, you might decide to copy every propert over from one object to another.

- This makes one object behave as if it has all the properties of the other object, by delegating the failed lookups from the first object to the second one.

```
var gold = {a:1};
log(gold.a); //1
log(gold.z); //undefined
```

### 1-time property copying
- helper functions
- copy all of the properties form one object onto another
```
var blue = extend({}, gold);
```
- doesn't come with JS
- will last indefinitely
- copying happens just at one moment during the program's execution
- not an ongoing copying back and forth behavior that keeps the two objects in sync
- a lookup for a property that isn't available on blue should result in undefined

### Prototype delegation
- rather than copying the properties over one by one, the idea would be to give the rose object some linkage to the gold object such that whenever a requested property can't be found on rose, it uses gold as sort of a fall back source of properties

### Object.create function
- can create objects that have delegation lookup feature
- just pass in desired fall back object
- will produce a new object that delegates field lookups to the fallback
```
var rose = Object.create(gold);
```
- when you ask that object for a property that can't be found directly on the object itself, the lookup falls through, up the chain to the prototype object
```
rose.b = 2;
log(rose.a); //1
```
- lookup will fall through rose and then is satisfied on the gold object and passed out as if the rose object had the property the whole time
- the apparent similarity between rose and gold is achieved at the very moment of lookup and not as a result of some earlier copying process
- for properties that can be found in the lower object, prototype chain is never consulted (not a failed lookup so the prototype relationship doesn't come into play)
- completely absent properties are reported missing, undefined

The difference between the two techniques relates to what moment you would expect the value present on gold to influence either of the other two objects. 

Single moment of copying or does it happen at every lookup event.

### Property lookup on cloned objects
```
gold.z = 3;
log(blue.z); //undefined
```
When we try to log a new property by consulting blue, no property is found there and since no delegation relationship exists, it can't look anywhere else for the other properties. Copy is just one time. So the relationship between gold and blue was over immediately. All that remains of those cloning efforts is the A property that we copied some time ago.

### Property lookup of delegated objects
```
log(rose.z); //3
```
When we go looking for a z property on the rose object, the failed lookup results in a fall through looup to the prototype object.

# Object Prototype
- provides the shared properties of all objects in the entire system
- when you ask an object for its dot to string property, you get access to a function that can do the appropriate work
```
rose.toString();
```
- once you've accessed the function, you can immediately call it
- the object that you did the property lookup on will appear to the left of the dot at that function's call time

# Constructor property
- makes it easy to tell what function was used to create a certain object
- points to a different object that's stored elsewhere
- object prototype vs constructor function

### Array prototype
- if you don't take any special steps, most new objects that you create will delegate to the object prototype
- some of the special objects that you can make in JS have extra features above and beyond the basic characteristics of all objects

##### Arrays
.indexOf
.slice
etc

These array methods are stored in another prototype called Array prototype. The array prototype has its own version of someof the standard methods like toString. The array prototype in turn delegates to the object prototype so that the non-unique parts of an array can be inherited from the object prototype.

Object prototype and array prototype both have constructor properties even though one delegates to the other.

# Conclusion
You should be able to use prototype chains to make objects that look very similar to other objects which is a useful technique for code sharing and for saving memory.
