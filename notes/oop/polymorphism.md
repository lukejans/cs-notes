# Polymorphism

> Meaning "many forms", is a concept in type theory that allows different types to be treated in a uniform way.

## Types

Java is a **strongly typed** language, which means that the type of a variable cannot be changed at runtime. This can make it difficult to write code that is flexible and reusable. So we can use **_polymorphism_** to improve this situation allowing us to handle different types in a uniform way without having to write separate code for each type.

### Subtypes & Supertypes

A class defines a **type** and can be used to create objects. Classes can have **subtypes** (classes that extend them) and **supertypes** (classes that they extend). _A variable of type `T` can hold references to subtypes but not supertypes_.

```Java
// NOTE: not all methods and variables are
//       implemented for simplicity

// type geometric object
class GeometricShape {
  void setSize(int size) { this.size = size; }
}

// subtype rectangle
class Rectangle extends GeometricShape {
  void draw(GraphicsContext gc) {}
  int getWidth() { return width; }
}

// subtype square
class Square extends Rectangle {
  void draw(GraphicsContext gc) {}
}

// subtype circle
class Circle extends GeometricShape {
  void draw(GraphicsContext gc) {}
  int getRadius() { return radius; }
}

GeometricShape foo = new Circle();
```

### Casting

In the above example, `foo` the **declared type** is `GeometricShape` but the **actual type** is `Circle`. You can only directly access the fields and methods of an object's declared type. To access the fields and methods of an objects actual type you have to **cast** it.

```Java
// accessing fields and methods on the declared type
foo.setSize(10); // valid
foo.getRadius(); // error

// accessing fields and methods on the actual type
((Circle) foo).getRadius(); // valid
((Circle) foo).setSize(10); // also valid
```

### What Method is called

In the above example it is an error to call `getRadius()` on `foo` as its declared type is `GeometricShape` which has no `getRadius()` method thus casting is needed.

What if the declared type and the actual type both have a method with the same name? In this case, calling the method is not an error because the declared type has the method, but instead of calling that method, it calls the actual type's method.

```Java
Square bar = new Square();

bar.draw(); // calls the Square draw method instead
            // of calling the Rectangle draw method
```

### Handling Different Types

The nice thing about having subtypes is that you can now store multiple different types in the same array or list.

```Java
// array containing many different shape types
GeometricShape[] shapes = new GeometricShape[10];

// ... some code that creates shapes and puts
//     them in the array.
```

Sometimes you don't know the subtype of an object and need to check the type before calling a method so you don't get a `ClassCastException`. This is likely to happen if you have list or array of objects. In this case you can use the `instanceof` operator to do this.

```Java
// some operation that needs to be performed on each shape
for(GeometricShape shape : shapes) {
  // check what subtype it is before casting
  if (shape instanceof Circle) {
    ((Circle) foo).getRadius();
  } else if (shape instanceof Rectangle) {
    ((Rectangle) foo).getWidth();
  }
}
```

## Abstract Classes & Methods

When designing a class hierarchy, superclasses should be more general and subclasses should be more specific. In some cases a class is so general that it should not be and sometimes cannot be used to directly create and instantiate objects. This is an **_abstract class_**, and is denoted by italics in a class diagram.

```Java
abstract class GeometricShape {
  abstract void draw();
}
```

Abstract classes are defined just like regular classes but have the following rules.

1. use the keyword `abstract` in their class header.
2. can have `abstract` methods.
3. cannot be instantiated to create objects.

Abstract methods are method headers with no bodies and also use the keyword `abstract` in their method header. These methods must be implemented by any class that extends the abstract class. These methods are also denoted by italicized text in a class diagram.

## Interfaces

Interfaces are like abstract classes except have the following rules:

1. use the keyword `interface` in their class header line instead of `class`.
2. all methods must be `abstract`.
3. cannot be instantiated to create objects.
4. All of their variables must be `static` `public` and `final` and they must be given a value when they are created.

Interfaces are used to define a contract that classes must adhere to and are obligated to implement the methods. Subclasses do not use `extends` on interfaces and instead use `implements`. In a class diagram interfaces appear in italics usually with the interface tag _\<\<interface\>\>_.

The header for the class Chicken in the above diagram looks like this:

```Java
public class Chicken extends Animal implements Edible {...}
```

Note that a class can only extend one other class, but it can implement multiple interfaces separated by commas. This gives you more flexibility in designing your class hierarchy. Here is an example of a class that implements multiple interfaces:

```Java
public class Chicken extends Animal implements Edible, Cool {...}
```

## The Comparable Interface

`Arrays.sort()` can be used to sort an array, and `Arrays.binarySearch()` can be used to efficiently search a sorted array. These methods requires a parameter of type `Comparable[]`. Comparable is an interface that forces the implementation of a `compareTo()` method. Whenever these methods have to compare two elements in the array, they do it by calling a `compareTo()` method.

These methods work for arrays of Strings because the `String` class implements the `Comparable` interface. If you have a class that implements `Comparable`, theses methods will work for your class as well. Here’s what the `Comparable` interface looks like in code:

```Java
public interface Comparable<E> {
  public abstract int compareTo(E o);
}
```

If you implement this interface, you must have a `compareTo()` method which compares the current object to the object passed as a parameter. This method returns a negative, zero or positive integer depending on whether your object is less than, equal to, or greater than the one passed as a parameter, respectively.

When you implement `Comparable` you have to replace every occurrence of `E` with the name of your class, like this:

```Java
public class MyClass implements Comparable<MyClass> {
  // ...

  public int compareTo(MyClass other) {
  // compare this to other here, and return the result.
  }

  // ...
}
```

Then if you have an array of type `MyClass`, it is also an array of type `Comparable` and you can sort it using `Arrays.sort()`.

Note that the `Comparable` interface forces you to implement this method, but it’s completely up to you how you do the comparison. For example if the class defines a Person, you could compare them by their first name, last name, age or some combination of the three. It all depends on what kind of sorting you want to do.
