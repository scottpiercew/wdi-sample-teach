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

#### JavaScript uses a different system — "inheriting" objects do not have functionality copied over to them, instead the functionality they inherit is linked to via the prototype chain (often referred to as prototypal inheritance).

When you try to access a property on the new object `George`, it checks the object’s own properties first. If it doesn’t find any there, it checks the `[[Prototype]]`, and so on up the prototype chain until it gets back to `Object.prototype`, which is the root delegate for most objects.

![prototype chain](https://user-images.githubusercontent.com/28062032/29120598-05bd1dc2-7cd9-11e7-8e09-a3ccf193a030.png)
_From [www.medium.com](https://medium.com/javascript-scene/3-different-kinds-of-prototypal-inheritance-es6-edition-32d777fa16c9)_


### Benefits 
- It's simple and powerful.
- It leads to smaller, less redundant code.
- It's dynamic and hence it's better for dynamic languages.
- Method delegation can preserve memory resources because you only need one copy of each method to be shared by all instances.

### Three different kinds of prototypal inheritance offers lots of flexibility:

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

  > * Functional inheritance makes use of a factory function, and then tacks on new properties using concatenative inheritance.

</details>

## Prototypal Inheritance Demo (5 mins)

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

All functions automatically get initialized with a prototype object. In the example above, we tacked a function onto it called `bark`.

```
function Dog() {
}

Dog.prototype.bark = function() {
 console.log(‘woof!’);
};

var fido = new Dog();

fido.bark(); // ‘woof!’
```

By placing `bark` on `Dog.prototype`, we made it available to all instances of `Dog`.

### Differential Inheritance

Methods aren’t copied from parent to child. Instead, children have an “invisible link” back to their parent object.

For example, `fido` doesn’t actually have its own method called `bark()` (in other words, `fido.hasOwnProperty(‘bark’) === false`).

What actually happens when I write `fido.bark()` is this:
1. The JS engine looks for a property called `bark` on our `fido` object.
2. It doesn’t find one, so it looks “up the prototype chain” to fido’s parent, which is `Dog.prototype`.
3. It finds `Dog.prototype.bark`, and calls it with this bound to `fido`.

<details>

  <summary><strong>Said another way...</strong></summary>

  > * There’s really no such property as fido.bark. It doesn’t exist. Instead, fido has access to the bark() method on Dog.prototype because it’s an instance of Dog. This is the “invisible link” I mentioned. More commonly, it’s referred to as the “prototype chain”.
</details>


#### How do we create an object in JavaScript that inherits from another object?

### Object.create()

```
var parent = {
 foo: function() {
 console.log(‘bar’);
 }
};

var child = Object.create( parent );

child.hasOwnProperty(‘foo’); // false
child.foo(); // ‘bar’
```

We created a new, empty object that has parent in its prototype chain. That means that even though child doesn’t have its own foo() method, it has access to the foo() method from parent.

## Putting It All Together Code Along (5 mins)

Create a Rectangle constructor.
```
function Rectangle( width, height ) {
 this.width = width;
 this.height = height;
}
```

When a function is used as a constructor, this refers to the new object that you’re creating. So in our Rectangle constructor, we’re taking width and height as arguments, and assigning those values to the width and height properties of our new Rectangle instance.

```
var rect = new Rectangle( 3, 4 );

rect.width; // 3
rect.height; // 4
```

Create a method for our Rectangle called area.

```
Rectangle.prototype.area = function() {
 return this.width * this.height;
};
```

```
var rect = new Rectangle( 3, 4 );

rect.area(); // 12
```

### Subclassing

What if we want to make a new class of object that inherits from Rectangle? Let’s say we need a class called Square.

```
function Square( length ) {
 this.width = this.height = length;
}
```

How do we make Square inherit from Rectangle? It’s all about setting up the prototype chain.
We can use Object.create() to create an empty object that inherits from another object. In the case of Square, that means all we need to do is this:

```
Square.prototype = Object.create( Rectangle.prototype );
```

All instances of Square will automatically have Square.prototype in their prototype chain, and because Square.prototype has Rectangle.prototype in its prototype chain, every Square will have access to the methods of Rectangle.

```
var square = new Square( 4 );

square.area(); // 16
```


## Conclusion (2 mins)

- Demonstrate a use case that explains prototypal inheritance and what kind of flexibility it gives to programmers 
- Use namespaces to organize application code 
- Define a custom constructor method that sets one or more properties of a new object 
