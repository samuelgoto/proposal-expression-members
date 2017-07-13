# Expression-bodied members

This is a [stage 0 proposal](https://tc39.github.io/process-document/) to add a syntactical simplification for expression-bodied members.

# Motivation

```javascript
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  // This feature enables a syntactical simplification for short
  // expression-bodied members. For example, one can write:
  area => this.width * this.height;
  perimeter => 2 * (this.width + this.height);
  toString() => `Rectangle: width=${this.width}, height=${this.height}`;

  // As opposed to the more verbose (but semantically equivalent) version:
  //
  // get area() { 
  //   return this.width * this.height;
  // }
  // get perimeter() {
  //   return 2 * (this.width + this.height);
  // }
  //
  // toString() {
  //   return `Rectangle: area=${this.area}, perimeter=${this.perimeter}`;
  // }
}

var shape = new Rectangle(2, 4);
console.log(shape.area); // 8
console.log(shape.perimeter); // 12
console.log(shape.toString()); // Rectangle: area=8, perimeter=12
```

# Examples

```javascript
class Person {
  firstName = "Sam";
  lastName = "Goto";
  dateOfBirth = new Date("05/02/1982");

  // This feature enables a syntactical simplification for short
  // expression-bodied members. For example, one can write:

  fullName => `${this.firstName} ${this.lastName}`;
  age => new Date().getFullYear() - this.dateOfBirth.getFullYear();
  toString() => `Name: ${fullName}, Age: ${age}`;

  // As opposed to the more verbose (but semantically equivalent) version:
  //
  // get fullName() { 
  //   return `${this.firstName} ${this.lastName}`;
  // }
  // get age() {
  //   return new Date().getFullYear() - this.dateOfBirth.getFullYear();
  // }
  //
  // toString() {
  //   return `Name: ${fullName}, Age: ${age}`;
  // }
}

var sam = new Person();
console.log(sam.fullName); // Sam Goto
console.log(sam.age); // 34
console.log(sam.toString()); // Name: Sam Goto, Age: 34
```

# Prior Art

## [C#'s Expression-bodied members](https://msdn.microsoft.com/en-us/magazine/dn802602.aspx)

```c#
public class Rectangle {
  public int Length { get; set; }
  public int Width { get; set; }

  public int Area => Length * Width;
  public int Perimeter => 2 * (Length + Width);

  // eliminated a wee bit o'syntax here
  public override string ToString() => $"Rectange: Length={Length}, Width={Width}";
}
```

## [Kotlin's Single-Expression Functions](https://kotlinlang.org/docs/reference/functions.html#single-expression-functions)

```kotlin
// When a function returns a single expression, the curly braces 
// can be omitted and the body is specified after a = symbol

fun double(x: Int): Int = x * 2
```

# Related Work

* Arrow functions
* Class members
* Getters/Setters for classes
