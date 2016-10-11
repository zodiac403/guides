# JavaScript Primer

While ES2015 becomes more ubiquitous each passing day,
not every developer has had the chance to dive into the new capabilities of the language.

In this guide we will be going over some of the features introduced by ES2015 and up,
and how to use them in the context of an Ember application.

## Properties

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

## `const`, `let`

-> const binding

```javascript
const a = "hello";
a = "bye"; // error
```

This is fine because you aren't changing the binding, that is, the value of `a` itself doesn't change.

```javascript
const a = { greeting: "good morning" };
a.greeting = "good night";
```

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