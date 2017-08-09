# Prototypes

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

## An Intro to Prototypes (5 mins)


Some people think JavaScript is not a true object-oriented language. In "classic OO" languages, you tend to define class objects of some kind, and you can then simply define which classes inherit from which other classes. JavaScript uses a different system — "inheriting" objects do not have functionality copied over to them, instead the functionality they inherit is linked to via the prototype chain (often referred to as prototypal inheritance).

<details>

  <summary><strong>How do we create an object in JavaScript that inherits from another object?</strong></summary>

  > * The Object.create() method creates a new object with the specified prototype object and properties.

</details>

```
Object.create(proto[, propertiesObject])
```

