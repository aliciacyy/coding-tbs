---
label: Scala
---

## Basics


### Values

Syntax for declaring a value:
```
val x: Int = 42
```
- `val` is immutable
- Types of `val` are optional as compiler can infer types
- Semicolons are allowed but not necesary


### Types
- String
- Boolean
- Char
- Int
- Short
- Long
- Float
- Double

### Variables
```
var variable: Int = 4
```
- Can be reassigned (mutable)
- Prefer vals over vars
- All vals and vars have types
- Changing variable is side effects

### Instruction vs Expression
- Instruction: Tells what to do (executed)
- Expression: Has a value and/or type (evaluated)
- In Scala, every single code will compute a value

```
val condition = if (true) 5 else 3
```
- `If` expression gives back a value
- `If` in Scala is an expression'
- Loops are discouraged in Scala as they introduce side-effects and specific to imperative programming
- Everything in Scala is an expression

### Unit
- Special type in Scala which is similar to `void`
- Doesn't return anything, can only hold the value `()`
- Side effects in Scala will return Unit

### Side effects examples
- Printing to console
- While loops
- Reassigining

### Code blocks
```
val codeBlock = {
    val y = 2
    val z = y + 1
    if (z > 2) "hello" else "goodbye"
}
```
- Code block is an expression
- Value of a  block is the value of the last expression

### Functions
Syntax:
```
def aFunction(a: String, b: Int): String =
    a + " " + b
```
- Calling a function is also an expression
- Parameterless functions can be called with just the name

"Loops"
```
def repeatFunction(a: String, n: Int): String = {
    if (n == 1) a
    else aString + repeatFunction(a, n-1)
}
```
- In Scala, use recursion
- Return type needs to be defined from recursive function
- Can use Unit as return type
- Can define functions inside function code blocks

Examples:
```
def factorial(n: Int): Int = 
  if (n <=0) 1
  else n * factorial(n-1)
```

```
def fibonacci(n: Int): Int = 
  if (n <=2) 1
  else fibonacci(n-1) + fibonacci(n-2)
```

```
def isPrime(n: Int): Boolean =
  def isPrimeUntil(t: Int): Boolean =
    if (t <= 1) true
    else n % t != 0 && isPrimeUntil(t-1)
  isPrimeUntil(n / 2)
```

### Recursion

Improved factorial
```
def factorial(n: Int): Int = }
    def factHelper(x: Int, accumulator: Int): Int =
        if (x<=1) accumulator
        else factHelper(x-1, x*accumulator)
    factHelper(n, 1)
```
Tail recursion
- Use recursive call as the last expression
- Add annotation `@tailrec` to check if it is a tail recursion

```
def isPrime(n: Int): Boolean = {
    def isPrimeTailrec(t: Int, isStillPrime: Boolean): Boolean =
        if (!isStillPrime) false
        else if (t <= 1) true
        else isPrimeTailrec(t-1, n%t != 0 && isStillPrime)
    isPrimeTailrec(n/2, true)
}
```

```
def fibo(n: Int): Int = {
    def fiboTail(i: Int, last: Int, nextToLast: Int): Int =
        if (i >= n) last
        else fiboTail(i+1, last + nextToLast, last)
    if (n<=2) 1
    else fiboTail(2,1,1)
}
```

### Call by name vs Call by value
```
def callByName(x: => Long)
```
- `=>` means call by name
- by value: value is computed before call and same value is used everywhere
- by name: expression is evaluated at every use

### Default and named arguments

```
def factHelper(x: Int, accumulator: Int = 1): Int =
    if (x<=1) accumulator
    else factHelper(x-1, x*accumulator)
```
- set default value of accumulator so can just call factHelper(10)

```
def pic(format: String = "jpg", width: Int, height: Int): Unit = println("test")

pic(width = 800)
```
- Can even pass with different order with named parameters

### Strings
- str.charAt(2)
- str.substring(7, 11)
- str.split(" ")
- str.startsWith("Hello")
- str.replace(" ", "-")
- str.toLowerCase()
- str.length
- str.toInt
- prepending and appending: `'a' +: str :+ 'z'`
- str.reverse
- str.take(2)

**S-interpolators**
```
val name = "John"
val age = 12

val greeting = s"Hello, my name i $name and I am $age years old"
val greeting2 = s"Hello, my name i $name and I am ${age + 1} years old"
```

** F-interpolators **
```
val speed = 1.2f
val myth = f"I can eat $speed%2.2f"
```
- 2 characters total minimum
- 2 characters precision

** Raw interpolator **
println(raw"This is a \n newline")
- injected variables still get escaped

## Object-Orienteed Programming
Define a class:

```
class Person(name: String, age: Int) {
    // can do anything inside, this block is evaluated on instiantiaion
    val x = 2 // this is a field

    def greet(name: String) Unit = println(s"$this.name says hi, $name")

    // more constructors
    def this(name: String) = this(name, 0)
}
```
``` 
val person = new Person("John", 24)
person.x
person.greet("Jane")
```
- Class parameters are not fields
- To add as field, change param to `val age: Int`

```
class Writer(firstName: String)
```

### Infix/operator notation
Only works with methods with only 1 parameter

e.g.
```
mary.likes("Inception")
mary likes "Inception"
```
All operators are methods.

### Prefix notation
All about unary operators.

unvary_ prefix only works with - + ~ !

```
!mary
mary.unary_!
```

### Postfix notation
For methods with no parameters. Rarely used in practice.
```
mary.isAlive
mary isAlive
```

### Apply
Need to define a method called `apply`

```
mary.apply() same as
mary()
```

### Class level functionality
Scala does not have class level functionality ("static")
```
// DONT HAVE THIS
class Person {
    public static final int N_EYES = 2
}
```
```
// USE THIS
object Person {
    val N_EYES = 2
}
```
Objects do not receive parameters.

Scala object is a singleton instance.

Objects are in their own class

### Companions
Can write `object Person` and `class Person` to separate singleton stuff.

Can access each other's private members

### Scala Applications
Scala object with `def main(args: Array[String]): Unit` or `extends App`

Need to pass in constructor arguments to parent class

Derived classes can override members or methods

Reuse parent fileds/methods with super

### Prevent inheritance with `final` and `sealed`
- use final on member
- use final on the entire class
- seal the class (can extend classes in this file only, prevents extension in other files)

### `abstract` classes and `traits`
- traits do not have constructor parameters
- multiple traits may be inherited by the same class
- traits = behaviour, abstract class = "thing"

Inheriting from a class and multiple traits

### Generics
```
class MyList[A]
class MyMap[Key, Value]
```

```
object MyList {
    def empty[A]: MyList[A] = ???
}
```

### Covariance
```
class CoList[+A]
val list: CoList[Animal] = new CoList[Cat]
```

### Invariance
```
class CoList[A]
val list: CoList[Animal] = new CoList[Animal]
```

### Contravariance
```
class CoList[-A]
val list: CoList[Cat] = new CoList[Animal]
```

### Bounded types
Restrict only for subclass of animal
```
class Cage[A <: Animal](animal: A)
```
Restrict only for superclass of animal
```
class Cage[A >: Animal](animal: A)
```

### case
```
case Class Person(name: String, age: Int)
```
Quick lightweight data structures with little boilerplate

- Class parameters are fields
- Sensible toString
- Equals and hashcode implemented out of the box
- Have copy method `copy()`
- Have companion objects
- Serializable
- Have extractor patterns = can be used in pattern matching

### Throw exceptions
```
throw new NullPointerException
```

### Catch exceptions
```
try {
    // code that might fail
} catch {
    case e: RuntimeException => println("caught")
} finally {
    // code that runs no matter what
}
```

### Define own exceptions
```
class MyException extends Exception
val expcetion = new MyException
throw exception
```

### Packages
A group of definitions under the same name

To use a definition, be in the same package or import the package

Best practice - mirror the file structure

`package object`s hold standalone methods/constants (one per package)

Name aliasing imports
```
import java.sql.{Date => SqlDate}
```