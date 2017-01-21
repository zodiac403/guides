# JavaScript Primer

While the Guides [assume you have a working knowledge of JavaScript](/#toc_assumptions),
using the language in the context of a new framework can be confusing,
especially if you are newer to the ecosystem.

On top of that, the [EcmaScript 2015](https://developer.mozilla.org/en/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla) (also known as ES6) and following specifications have introduced features to JavaScript that developers may have not had a chance to get familiar with yet.

In this guide we will be covering some common JavaScript code patterns that appear in Ember applications,
so you can get a clearer sense of where the language ends and the framework starts.

## `var`, `let`, `const`

For a long while, the way to declare a variable in JavaScript was using `var`:

```javascript
var greeting = "Hello World";
```

But when the ES2015 specification was released, two new ways were introduced,
`let` and `const`.
I'll first explain how `let` and `const` are different from `var`,
and then a detail about `const`.

### Lexical scoping

`const` and `let` are called 

-> `const` binding

```javascript
const a = "hello";
a = "bye"; // error
```

This is fine because you aren't changing the binding, that is, the value of `a` itself doesn't change.

```javascript
const a = { greeting: "good morning" };
a.greeting = "good night";
```

## Object properties

One quirk of the JavaScript language that commonly trips up developers if that if you define an array or object property directly in your class,
every instance of that class will share the same array/object.
Let's look at an example to make it clearer.

We will start with a Framework class, with a string `language` property, and a versions array.
If you are not familiar with the `class` syntax, you can read about it on [the MDN reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
We will be using the `class` syntax, if you are not familiar you can read more on 
We'll then create two instances of that class, `ember` and `phoenix`.

```javascript
const Framework = Object.create({
  language: 'JavaScript',
  versions: []
});

let ember = Object.create(Framework);
let phoenix = Object.create(Framework);
```




```javascript
export default Ember.Component.extend({
  todos: [
    …
  ]
});
```

```javascript
export default Ember.Component.extend({
  todos: null,
  
  init() {
    this._super(...arguments);
    this.todos = [
      …
    ]
  }
});
```

## Modules

-> bit of background. when, how, who worked on it

-> one file == one module

-> imports

-> exports


## Arrow functions

Arrow functions are not a short-hand.

```javascript
let obj = Ember.Object.create({
    firstName: "Robert",
    lastName: "Jackson",
    
    getName: () => {
    }
});
```


## Method literal short-hand

```javascript
export default Ember.Route.extend({
  model: function() {
    return [];
  }
});
```

```javascript
export default Ember.Route.extend({
  model() {
    return [];
  }
});
```

## Object literal short-hand

```javascript
let firstName = "Robert";
let lastName = "Jackson";

let person = {
  firstName: firstName,
  lastName: lastName
};
// => { firstName: 'Robert', lastName: 'Jackson' }
```

```javascript
let firstName = "Robert";
let lastName = "Jackson";

let person = {
  firstName,
  lastName
};
// => { firstName: 'Robert', lastName: 'Jackson' }
```

## Destructuring

```javascript
let obj = { firstName: "Robert", lastName: "Jackson", alias: "rwjblue" };
let { firstName, lastName } = obj;

console.log(firstName);
// -> Robert
console.log(lastName);
// -> Jackson
```

Beware of destructuring Ember.Objects, you need to do `getProperties`:

```javascript
let obj = Ember.Object.create({ firstName: "Robert", lastName: "Jackson", alias: "rwjblue" });
let { firstName, lastName } = obj.getProperties('firstName', 'lastName');

console.log(firstName);
// -> Robert
console.log(lastName);
// -> Jackson
```

## Template strings

```javascript
let firstName = "Robert";
let lastName = "Jackson";

console.log("My name is " + firstName + " " + lastName + ".");
```

```javascript
let firstName = "Robert";
let lastName = "Jackson";

console.log(`My name is ${firstName} ${lastName}.");
```

Useful in computed properties. Example:

```javascript
export default Ember.Object.extend({
  firstName: "Robert",
  lastName: "Jackson",

  fullName: Ember.computed('firstName', 'lastName', function() {
    let { firstName, lastName } = this.getProperties('firstName', 'lastName');

    return `My name is ${firstName} ${lastName}.`;
  })
});
```

## Default, rest, spread

```javascript
export default Ember.Service.extend({
  init() {
    this._super(...arguments);
  }
});
```
