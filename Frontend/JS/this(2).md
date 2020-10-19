# Understanding JavaScript Function Invocation and "this"

`this`는 자바스크립트에서 꽤 어려운 개념이다. 
우선 자바스크립트의 함수는 기본적으로 객체이다. 

함수의 호출은 아래와 같다. 

`fn.call(window [ES5-strict: undefined], ...args)`
=== `fn(...args)`와 같다. 

후자의 경우가 sugar된 문법이라고 보면 된다.

실제 spec에는 call이 아닌 `[[call]]` 이라는 내부 메서드에 의해서 동작된다. 

함수 호출에 대해 알아보면서 `this`를 깊이 이해해보자. 

## The Core Primitive

First, let's look at the core function invocation primitive, a Function's call method[1]. The call method is relatively straight forward.
`func.call([thisArg[, arg1, arg2, ...argN]])`

1. Make an argument list (argList) out of parameters 1 through the end
2. The first parameter is thisValue
3. Invoke the function with this set to thisValue and the argList as its argument list
For example:

```js
function hello(thing) {
  console.log(this + " says hello " + thing);
}

hello.call("pius", "world") //=> pius says hello world
```

hello 메서드를 "pius"로 설정된 `this`와 "world" 인자로 호출한다. 

As you can see, we invoked the hello method with this set to "Yehuda" and a single argument "world". This is the core primitive of JavaScript function invocation. You can think of all other function calls as desugaring to this primitive. (to "desugar" is to take a convenient syntax and describe it in terms of a more basic core primitive).

[1] In the ES5 spec, the call method is described in terms of another, more low level primitive, but it's a very thin wrapper on top of that primitive, so I'm simplifying a bit here. See the end of this post for more information.

Simple Function Invocation
Obviously, invoking functions with call all the time would be pretty annoying. JavaScript allows us to invoke functions directly using the parens syntax (hello("world"). When we do that, the invocation desugars:

function hello(thing) {
  console.log("Hello " + thing);
}

// this:
hello("world")

// desugars to:
hello.call(window, "world");
1
2
3
4
5
6
7
8
9
This behavior has changed in ECMAScript 5 only when using strict mode[2]:

// this:
hello("world")

// desugars to:
hello.call(undefined, "world");
1
2
3
4
5
The short version is: a function invocation like fn(...args) is the same as fn.call(window [ES5-strict: undefined], ...args).

Note that this is also true about functions declared inline: (function() {})() is the same as (function() {}).call(window [ES5-strict: undefined).

[2] Actually, I lied a bit. The ECMAScript 5 spec says that undefined is (almost) always passed, but that the function being called should change its thisValue to the global object when not in strict mode. This allows strict mode callers to avoid breaking existing non-strict-mode libraries.

Member Functions
The next very common way to invoke a method is as a member of an object (person.hello()). In this case, the invocation desugars:

```js
var person = {
  name: "Brendan Eich",
  hello: function(thing) {
    console.log(this + " says hello " + thing);
  }
}

// this:
person.hello("world")

// desugars to this:
person.hello.call(person, "world");
```

Note that it doesn't matter how the hello method becomes attached to the object in this form. Remember that we previously defined hello as a standalone function. Let's see what happens if we attach is to the object dynamically:

```js
function hello(thing) {
  console.log(this + " says hello " + thing);
}

person = { name: "Brendan Eich" }
person.hello = hello;

person.hello("world") // still desugars to person.hello.call(person, "world")

hello("world") // "[object DOMWindow]world"
```

Notice that the function doesn't have a persistent notion of its 'this'. It is always set at call time based upon the way it was invoked by its caller.

## Using Function.prototype.bind
Because it can sometimes be convenient to have a reference to a function with a persistent this value, people have historically used a simple closure trick to convert a function into one with an unchanging this:

```js
var person = {
  name: "Brendan Eich",
  hello: function(thing) {
    console.log(this.name + " says hello " + thing);
  }
}

var boundHello = function(thing) { return person.hello.call(person, thing); }

boundHello("world");
```

Even though our boundHello call still desugars to boundHello.call(window, "world"), we turn right around and use our primitive call method to change the this value back to what we want it to be.

We can make this trick general-purpose with a few tweaks:
```js
var bind = function(func, thisValue) {
  return function() {
    return func.apply(thisValue, arguments);
  }
}

var boundHello = bind(person.hello, person);
boundHello("world") // "Brendan Eich says hello world"
```

In order to understand this, you just need two more pieces of information. First, arguments is an Array-like object that represents all of the arguments passed into a function. Second, the apply method works exactly like the call primitive, except that it takes an Array-like object instead of listing the arguments out one at a time.

Our bind method simply returns a new function. When it is invoked, our new function simply invokes the original function that was passed in, setting the original value as this. It also passes through the arguments.

Because this was a somewhat common idiom, ES5 introduced a new method bind on all Function objects that implements this behavior:

var boundHello = person.hello.bind(person);
boundHello("world") // "Brendan Eich says hello world"
1
2
This is most useful when you need a raw function to pass as a callback:

var person = {
  name: "Alex Russell",
  hello: function() { console.log(this.name + " says hello world"); }
}

$("#some-div").click(person.hello.bind(person));

// when the div is clicked, "Alex Russell says hello world" is printed

This is, of course, somewhat clunky, and TC39 (the committee that works on the next version(s) of ECMAScript) continues to work on a more elegant, still-backwards-compatible solution.
