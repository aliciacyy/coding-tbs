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

**F-interpolators**
```
val speed = 1.2f
val myth = f"I can eat $speed%2.2f"
```
- 2 characters total minimum
- 2 characters precision

**Raw interpolator**
```
println(raw"This is a \n newline")
```
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
- Objects do not receive parameters.
- Scala object is a singleton instance.
- Objects are in their own class

### Companions
- Can write `object Person` and `class Person` to separate singleton stuff.
- Can access each other's private members

### Scala Applications
- Scala object with `def main(args: Array[String]): Unit` or `extends App`
- Need to pass in constructor arguments to parent class
- Derived classes can override members or methods
- Reuse parent fileds/methods with super

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
- A group of definitions under the same name
- To use a definition, be in the same package or import the package
- Best practice - mirror the file structure

`package object`s hold standalone methods/constants (one per package)

Name aliasing imports
```
import java.sql.{Date => SqlDate}
```

## Functional Programming
### Functions
All Scala functions are objects
- Function traits up to 22 params
```
val doubler = new MyFunction[Int, Int] {
    override def apply(element: Int): Int = element * 2
}
println(doubler(2))

trait MyFunction[A, B] {
    def apply(element: A): B
}
```

### Anonymous functions
```
var doubler = (x: Int) => x * 2

var adder: (Int, Int) => Int = (a: Int, b: Int) => a + b

val doSomething: () => Int () => 3

val fancy: Int => Int = _ + 1 // same as x => x + 1
```

### Higher order functions (HOF)
- Functions that either take in other functions as parameters or returns a function as result 
- Examples: map, flatMap, filter

```
// function that applies a function n times over a value x
// nTimes(f, n, x)
// nTimes(f, 3, x) = f(f(f(x))) = nTimes(f, 2, f(x)) = f(f(f(x)))
// nTimes(f, n, x) = f(f(...f(x))) = nTimes(f, n-1, f(x))
def nTimes(f: Int => Int, n: Int, x: Int): Int =
    if (n <= 0) x
    else nTimes(f, n-1, f(x))

val plusOne = (x: Int) => x + 1
println(nTimes(plusOne, 10, 1))

// ntb(f,n) = x => f(f(f...(x)))
// increment10 = ntb(plusOne, 10) = x => plusOne(plusOne....(x))
// val y = increment10(1)
def nTimesBetter(f: Int => Int, n: Int): (Int => Int) =
    if (n <= 0) (x: Int) => x
    else (x: Int) => nTimesBetter(f, n-1)(f(x))

val plus10 = nTimesBetter(plusOne, 10)
println(plus10(1))
  ```

### Curried functions
- Functions with multiple parameter lists
```
// receives an Int and returns another function
val superAdder: Int => (Int => Int) = (x: Int) => (y: Int) => x + y
val add3 = superAdder(3)  // y => 3 + y
add3(10) // or
superAdder(3)(10)
```
- Useful when you want to define helper functions that you want to use later on various values

### flatMap
```
list = List(1,2,3)
val toPair = (x: Int) => List(x, x+1)
println(list.flatMap(toPair))
// 1, 2, 2, 3, 3, 4

// print all combinations between two lists
val numbers = List(1,2,3,4)
val chars = List('a','b','c','d')
val colors = List("black", "white")

// List("a1", "a2"... "d4")
```

### for-comprehensions
```
// for-comprehensions
val forCombinations = for {
    n <- numbers if n % 2 == 0
    c <- chars
    color <- colors
} yield "" + c + n + "-" + color
println(forCombinations)
```

### Sequenecs: List, Array, Vector
**Sequence**
- General interface for DS that have a well defined order and can be index
- e.g. `val seq = Seq(1,2,3,4)
- `seq ++ Seq(5,6,7)`
- Range: `val range: Seq[Int] = 1 until 10

**List**
- Immutable linked list
- head, tail, isEmpty are O(1)
- Other operations are O(n)

```
val aList = List(1,2,3)
val prepended = 42 +: aList :+ 89
val apples5 = List.fill(5)("apple")
println(aList.mkString("-|-"))
```

**Arrays**
- Can be manually constructed with predefined lengths
- Can be mutated
- Indexing is fast
```
val numbers = Array(1,2,3,4)
val threeElements = Array.ofDim[String](3)
// mutation
numbers(2) = 0  // syntax sugar for numbers.update(2, 0)
```

**Vector**
- Immutable sequence
- Indexed read and write 
- Fast element addition
```
val vector: Vector[Int] = Vector(1,2,3)
```

### Tuples and maps
**Tuples**
- Finite ordered "lists"
- 1 indexed
```
// tuples = finite ordered "lists"
val aTuple = (2, "hello, Scala")  // Tuple2[Int, String] = (Int, String)

println(aTuple._1)  // 2
println(aTuple.copy(_2 = "goodbye Java"))
println(aTuple.swap)  // ("hello, Scala", 2)
```

**Maps**
```
// Maps - keys -> values
val aMap: Map[String, Int] = Map()

val phonebook = Map(("Jim", 555), "Daniel" -> 789, ("JIM", 9000)).withDefaultValue(-1)
// a -> b is sugar for (a, b)
```

### Options
- Wrapper for a value that may be present or not
- Use to avoid NPEs and null-related assertions
```
// chained methods
def backupMethod(): String = "A valid result"
val chainedResult = Option(unsafeMethod()).orElse(Option(backupMethod()))

// DESIGN unsafe APIs
def betterUnsafeMethod(): Option[String] = None
def betterBackupMethod(): Option[String] = Some("A valid result")
val betterChainedResult = betterUnsafeMethod() orElse betterBackupMethod()
```

```
  /*
    if (h != null)
      if (p != null)
        return Connection.apply(h, p)
    return null
   */
  val connection = host.flatMap(h => port.flatMap(p => Connection.apply(h, p)))

  // chained calls
  config.get("host")
    .flatMap(host => config.get("port")
      .flatMap(port => Connection(host, port))
      .map(connection => connection.connect))
    .foreach(println)

  // for-comprehensions
  val forConnectionStatus = for {
    host <- config.get("host")
    port <- config.get("port")
    connection <- Connection(host, port)
  } yield connection.connect
  forConnectionStatus.foreach(println)
```

### Handling failures
- A Try is a wrapper for a computation that might fail or not
- Use to handle exception gracefully
```
val potentialFailure = Try(unsafeMethod())
def betterUnsafeMethod(): Try[String] = Failure(new RuntimeException)
def betterBackupMethod(): Try[String] = Success("A valid result")
val betterFallback = betterUnsafeMethod() orElse betterBackupMethod()

  // shorthand version
  HttpService.getSafeConnection(host, port)
    .flatMap(connection => connection.getSafe("/home"))
    .foreach(renderHTML)

  // for-comprehension version
  for {
    connection <- HttpService.getSafeConnection(host, port)
    html <- connection.getSafe("/home")
  } renderHTML(html)
```

## Pattern matching
```
val description = x match {
  case 1 => "the ONE"
  case 2 => "double or nothing"
  case 3 => "third time is the charm"
  case _ => "something else"  // _ = WILDCARD
}
```

```
// 1. Decompose values
case class Person(name: String, age: Int)
val bob = Person("Bob", 20)

val greeting = bob match {
  case Person(n, a) if a < 21 => s"Hi, my name is $n and I can't drink in the US"
  case Person(n, a) => s"Hi, my name is $n and I am $a years old"
  case _ => "I don't know who I am"
}
println(greeting)
```
- Cases are matched in order
- If no match found (and no default match), will get `scala.MatchError`

```
  // PM on sealed hierarchies
sealed class Animal
case class Dog(breed: String) extends Animal
case class Parrot(greeting: String) extends Animal

val animal: Animal = Dog("Terra Nova")
animal match {
  case Dog(someBreed) => println(s"Matched a dog of the $someBreed breed")
}
```

```
// 2.2 variable
val matchAVariable = x match {
  case something => s"I've found $something"
}


// 3 - tuples
val aTuple = (1,2)
val matchATuple = aTuple match {
  case (1, 1) =>
  case (something, 2) => s"I've found $something"
}

val nestedTuple = (1, (2, 3))
val matchANestedTuple = nestedTuple match {
  case (_, (2, v)) =>
}

// 4 - case classes - constructor pattern
// PMs can be nested with CCs as well
val aList: MyList[Int] = Cons(1, Cons(2, Empty))
val matchAList = aList match {
  case Empty =>
  case Cons(head, Cons(subhead, subtail)) =>
}

// 5 - list patterns
val aStandardList = List(1,2,3,42)
val standardListMatching = aStandardList match {
  case List(1, _, _, _) => // extractor - advanced
  case List(1, _*) => // list of arbitrary length - advanced
  case 1 :: List(_) => // infix pattern
  case List(1,2,3) :+ 42 => // infix pattern
}

// 6 - type specifiers
val unknown: Any = 2
val unknownMatch = unknown match {
  case list: List[Int] => // explicit type specifier
  case _ =>
}

// 7 - name binding
val nameBindingMatch = aList match {
  case nonEmptyList @ Cons(_, _) => // name binding => use the name later(here)
  case Cons(1, rest @ Cons(2, _)) => // name binding inside nested patterns
}

// 8 - multi-patterns
val multipattern = aList match {
  case Empty | Cons(0, _) => // compound pattern (multi-pattern)
}

// 9 - if guards
val secondElementSpecial = aList match {
  case Cons(_, Cons(specialElement, _)) if specialElement % 2 == 0 =>
}
```

---

**Code examples:** https://www.udemy.com/course/rock-the-jvm-scala-for-beginners/
