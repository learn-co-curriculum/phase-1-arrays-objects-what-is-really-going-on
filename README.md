# What's Really Going on With Arrays and Objects in JavaScript?

## Learning Goals

- Recognize Arrays are Objects
- Objects in JavaScript can store all sorts of values

## Introduction

So far, we've seen that both Arrays and Objects can store things inside
them, including _other_ Arrays and Objects. We think this is pretty cool!
You can use data to represent all sorts of things using nested data
structures. 

We'll soon see, however, that there is more going on. In this lesson, we're
going to briefly explore what's really going on with Arrays and Objects behind
scenes.

> **Note:** Before we dive in too deep - some of the topics we will touch on in
> this lesson will be covered in more depth later on.

## Arrays are... Objects in JavaScript?

If you recall from the previous lessons on functions, in JavaScript, functions
are considered _first-class_, which means, like data values, they can be used as arguments
in other functions and assigned to variables. It also means you can store functions _in_
Arrays and Objects. For example:

```js
const phrases = {
  greeting: "Hello there!",
  time: () => {
    const currentTime = new Date();
    return `The time is ${currentTime.getHours()}:${currentTime.getMinutes()}`
  }
}

phrases.greeting
// => "Hello there!"
phrases.time()
// => "The time is 16:51" (or whatever time it is currently on a 24-hour clock)
```

Here, we've stored a function in an Object, and then called that function with `phrases.time()`. Let's break that down - we first call the `phrases` object,
then a `.`, a dot. This is followed by the key, `time`. This key points to a
value - a function expression. Adding parentheses, `()` executes that function expression.

Now, hold on a moment - we've seen this syntax before, but with Arrays:

```js
const listOfGoodDogs = ["Peach", "Harpo", "Emma"]

listOfGoodDogs.map((dog) => console.log(dog))
// LOG: Peach
// LOG: Harpo
// LOG: Emma
```

Here, we've called `map` as a part of `listOfGoodDogs` and passed in a callback function
to log each element in the Array. `map` is acting like an Object key, just like `time`, pointing to a function expression.

Why does this work? Well... it is because Arrays _are_ Objects in JavaScript. Lots of things
are Objects, actually. Notice in the two previous examples, we used the dot syntax for
other things. In the first code snippet, we assigned a variable, `currentTime`, to `new Date()`, then
called `getHours()` and `getMinutes()` on it. In the second code snippet, we called `log()` as
part of `console`.

These are all JavaScript Objects - [Arrays][arrays] and other things like [`Date`][date] are Objects... even [_Strings_][strings] are Objects, which is why we can do things like `"hello".slice(1)`. Functions... are also Objects in JavaScript if things weren't confusing enough already.

As it turns out, Objects are a bit more complex than we originally presented! 

## A Deeper Look at Objects

Let's review what we know about Objects. Objects are data structures that act sort of like dictionaries. Like a dictionary contains words followed by their definition, Objects contain key/value pairs. We've told you Arrays are objects in JavaScript, though they are clearly a special type of Object. Now, Arrays can hold data values in a list, and we can create many different Arrays that store different values. Similarly, we can create plain old Objects that each contain something different. However, some 



We've gotten used to creating objects using the object literal notation, using curly braces to wrap comma separated key/value pairs.

```js
const phrases = {
  greeting: "Hello there!",
  time: () => {
    const currentTime = new Date();
    return `The time is ${currentTime.getHours()}:${currentTime.getMinutes()}`
  }
}
```

This way of creating Objects is often preferred due to its simplicity, but it also hides what is happening behinds the scenes. First, we want to be clear in the language we use - so far we've talked about key/value pairs in general, but they're actually referred to as different things depending on what they store. Key/value pairs, like `greeting` and `time`, are referred to as _properties_ of the object. Properties that store a function expression as a value, like `time`, are referred to as _methods_ of the object. The `phrases` object, then, has two properties we've defined.








The second thing we want to clarify is that the object literal notation is not the only
way to define an object. 

### Creating an Object Using the Constructor Function

We mentioned earlier that functions are Objects. The easiest way to demonstrate this is to
create an object using a function. We can recreate our `phrases` object using what is called a 'Constructor' function:

```js
function PhraseObjectConstructor() {
  this.greeting = "Hello there!";
  this.time = () => {
    const currentTime = new Date();
    return `The time is ${currentTime.getHours()}:${currentTime.getMinutes()}`
  };
}

const phrases = new PhraseObjectConstructor()


phrases.greeting
// => "Hello there!"
phrases.time()
// => "The time is 17:30"
```

We can see here that the code above results in a `phrases` object that behaves like the previous examples. You may notice some things that are unfamiliar, though.

Note that instead of using key/value pairs to set properties, we've used something else - `this` followed by the dot notation we've seen. We will go into greater depth on `this` and context later. Take note that in our example, `this` seems to be written like it is an Object itself; the properties we're assigning, `greeting` and `time`, are part of `this`.

Another noticeable difference is that `PhraseObjectConstructor()` does not _return_ anything explicitly (the only `return` is inside the `time` method). However, when we run `new PhraseObjectConstructor()`, we do assign _something_ to the `phrases` variable - _an Object_. 

The essential bit in this puzzle is [`new`][new]. Adding `new` before `PhraseObjectConstructor()` tells JavaScript to do a couple of things:

- It creates a basic Object (which gets assigned to the `phrases` variable)
- It binds `this` to the newly created Object. The properties defined in the function now belong to _this_ new Object
- It adds a new property, `__proto__` to the Object.

The first action is somethine we're familiar with




> **Note:** Remember, do not be discouraged if these things are confusing. They are most definitely confusing and will remain that way for a bit, but that is okay. As you progress through the JavaScript content, you'll see `this` and prototypes 







[new]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new 


we can think of `this` as referring to the _thing_ `this` is inside of.






[strings]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[arrays]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array
[date]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date


If you open Chrome dev tools and navigate to the Console, you can test for yourself - type `console` alone 

More than that, however, arrays and objects can store 


That's all great, but for this lesson, we're going to spend a little time
going deeper into what 

In JavaScript, 


But what is _really going on here?_ 
