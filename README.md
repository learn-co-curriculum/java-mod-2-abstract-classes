# Abstract Classes

## Learning Goals

- Explain abstract classes
- Create abstract classes

## Introduction

The classes that we have seen so far have had 3 basic properties:

1. They had variables (i.e. things that they are or that they have)
2. They had actions (i.e. things that they can do)
3. They could be instantiated (i.e. we could create variables based on them)

The `AnimalRunner` example from the previous section shows us how to instantiate
all our sample classes, including the base `Animal` class.

But what if we both a) still wanted to have a base `Animal` class, but also b)
didn't want anyone to be able to instantiate it? One could imagine for example
that although all animals have some things and behaviors in common, some things
or behaviors are specific to an actual type of animal. Consider the sound that
an animal makes - there is no "generic" sound that is applicable to all animals,
so if we wanted to give all our animals the ability to make a sound, but we
couldn't implement a "generic" version of the ability on the base `Animal`
class, we could make the `Animal` class `abstract`.

## Abstract Class in Java

An `abstract` class is a class that cannot be instantiated. It has to be
extended _and_ its abstract methods have to be implemented.

Let's examine that closer with our `Animal` class. We're going to make the
following changes:

- We want all animals to be able to make a sound
- We do not think there is a generic sound that applies to all animals, so we
  don't want the `Animal` class to have the ability to make any sound

Let's add the keyword `abstract` to the class definition:

```java
public abstract class Animal {
    // ...
}
```

Then let's add an abstract method named `makeSound`:

```java
    public abstract void makeSound();
```

An `abstract` method definition differs from a regular method in 2 ways:

1. It has the `abstract` keyword in its definition
2. It does not have any implementation code, so its signature is simply followed
   by a `;` to end the method definition

There is a 3rd difference that isn't evident from the method definition, but
that we mentioned before: an abstract class cannot be instantiated, so the
following statement in our `AnimalRunner` no longer compiles:

```java
        Animal baseAnimal = new Animal();
```

Essentially, the `Animal` class has now declared that it's "incomplete". It
wants to "make a sound", but it has not defined "how to make a sound", i.e. that
method has no implementation.

In order to be used, an `abstract` class must be extended and its `abstract`
methods must be implemented. For example, we can implement the `makeSound()`
method in our `Cat` class as follows:

```java
    public void makeSound() {
        System.out.println("Meow");
    }
```

The `Cat` class can now be instantiated and used like before, including its
`makeSound()` method:

```java
        Cat myCat = new Cat();
        myCat.takeBreath();
        myCat.useLitter();
        myCat.makeSound();
```

As you can see from the adjustment to our previous example, the `Animal` class
still has default behavior that applies to all animals, in this case the
`takeBreath()` method.

Abstract classes are used when default properties and behaviors need to be
defined for a specific type of object, but some behavior needs to be left
undefined by the base class and must be implemented by the subclasses. In our
case, that behavior was the ability to make a sound.

You may be thinking that an alternative to adding the new `abstract makeSound()`
method in the `Animal` class could have been to simply not add the method at all
and let each subclass add their own implementation. The problem with that
approach is that each subclass could decide for itself whether or not to have a
`makeSound()` method. Whereas what we want is to force all animals to have a
`makeSound()` method, without providing a base implementation for it.

We also want to establish that any `Animal` that doesn't make a sound is
"incomplete" and therefore cannot be used. So the `Animal` class cannot be
instantiated on its own and needs a subclass that implements the missing
functionality.
