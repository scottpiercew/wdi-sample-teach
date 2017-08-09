# Prototypal Inheritance in JavaScript

### Objectives
*After this lesson, students will be able to:*

- Demonstrate a use case that explains prototypal inheritance and what kind of flexibility it gives to programmers 
- Use namespaces to organize application code 
- Define a custom constructor method that sets one or more properties of a new object 

### Preparation
*Before this lesson, students should already be able to:*

- Understand Ruby-based OOP
- Use JavaScript variables, functions, objects, and callbacks

> Note: Solution code for this lesson is built out as the lesson progresses.

## An Intro to Prototypes (3 mins)


Some people think JavaScript is not a true object-oriented language. In "classic OO" languages, you tend to define class objects of some kind, and you can then simply define which classes inherit from which other classes. 

<details>

  <summary><strong>Syntactical sugar...</strong></summary>

  > * The class keyword is introduced in ES2015, but is syntactical sugar, JavaScript remains prototype-based

</details>

JavaScript uses a different system — "inheriting" objects do not have functionality copied over to them, instead the functionality they inherit is linked to via the prototype chain (often referred to as prototypal inheritance).

How do we create an object in JavaScript that inherits from another object?

We can use the different kinds of prototypal inheritance:

<details>

  <summary><strong>Differential Inheritance</strong></summary>

  > * A delegate prototype is an object that serves as a base for another object. When you inherit from a delegate prototype, the new object gets a reference to the prototype.

</details>
<details>

  <summary><strong>Concatenative Inheritance</strong></summary>

  > * Concatenative inheritance is the process of copying the properties from one object to another, without retaining a reference between the two objects. It relies on JavaScript’s dynamic object extension feature.

</details>
<details>

  <summary><strong>Functional Inheritance</strong> *(Not to be confused with functional programming)*</summary>

  > * Coined by Douglas Crockford in “JavaScript: The Good Parts”. Functional inheritance makes use of a factory function, and then tacks on new properties using concatenative inheritance.

</details>

## Prototypal Inheritance Demo (10 mins)

### Function prototypes
In JavaScript, all functions are also objects, which means that they can have properties. And as it so happens, they all have a property called `prototype`, which is also an object.
```
function foo() {
}
typeof foo.prototype // ‘object’
```
Any time you create a function, it will automatically have a property called prototype, which will be initialized to an empty object.

### Constructors

As a convention, functions that are meant to be used as constructors are generally capitalized.

```
function Dog() {
}
```

If I want to make an instance of Dog, I use the new keyword. Constructors — are using the function to construct a new object. Any time you see the new keyword, it means that the following function is being used as a constructor.

```
var fido = new Dog();
```

### Methods

```
function Dog() {
}
Dog.prototype.bark = function() {
 console.log(‘woof!’);
};
```

All functions automatically get initialized with a prototype object. In the example above, we tacked a function onto it called bark.

```
function Dog() {
}
Dog.prototype.bark = function() {
 console.log(‘woof!’);
};
var fido = new Dog();
fido.bark(); // ‘woof!’
```

By placing bark on Dog.prototype, we made it available to all instances of Dog.

### Differential Inheritance

Methods aren’t copied from parent to child. Instead, children have an “invisible link” back to their parent object.

For example, fido doesn’t actually have its own method called bark() (in other words, fido.hasOwnProperty(‘bark’) === false).

What actually happens when I write fido.bark() is this:
1. The JS engine looks for a property called bark on our fido object.
2. It doesn’t find one, so it looks “up the prototype chain” to fido’s parent, which is Dog.prototype.
3. It finds Dog.prototype.bark, and calls it with this bound to fido.

<details>

  <summary><strong>Said another way...</strong></summary>

  > * There’s really no such property as fido.bark. It doesn’t exist. Instead, fido has access to the bark() method on Dog.prototype because it’s an instance of Dog. This is the “invisible link” I mentioned. More commonly, it’s referred to as the “prototype chain”.
</details>


## Conclusion (2 mins)

- Demonstrate a use case that explains prototypal inheritance and what kind of flexibility it gives to programmers 
- Use namespaces to organize application code 
- Define a custom constructor method that sets one or more properties of a new object 
