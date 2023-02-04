---
label: Scala
---

### Option

We can test whether an Option is Some or None using these following methods:

- isDefined – true if the object is Some
- nonEmpty – true if the object is Some
- isEmpty – true if the object is None

We can retrieve the Option‘s value via the get method. If we invoke the get method on an instance of None, then a NoSuchElementException will be thrown.

We also have a couple of other retrieval methods:

- getOrElse – Retrieve the value if the object is Some, otherwise return a default value
- orElse – Retrieve the Option if it is Some, otherwise return an alternate Option

```Example
val o1: Option[Int] = Some(10)
assert(o1.map(_.toString).contains("10"))
assert(o1.map(_ * 2.0).contains(20))

val o2: Option[Int] = None
assert(o2.map(_.toString).isEmpty)
```

We can also do collection-style filtering on Options:

- filter – Returns the Option if the Option‘s value is Some and the supplied function returns true
- filterNot – Returns the Option if the Option‘s value is Some and the supplied function returns false
- exists – Returns true if the Option is set and the supplied function returns true
- forall – Same behavior as exists since Options have a maximum of one value

### Either

` Either[String, Int]`

Functions exactly similar to an Option. The only dissimilarity is that with Either it is practicable to return a string which can explicate the instructions about the error that appeared.

Right is similar to the Some class and Left is same as None class.

Left is utilized for the failure where, we can return the error occurred inside the child Left of the Either and Right is utilized for Success.

Either is right-biased, which means that Right is assumed to be the default case to operate on. If it is Left, operations like map and flatMap return the Left value unchanged.

```Example 1
import scala.io.StdIn._
val in = readLine("Type Either a string or an Int: ")
val result: Either[String,Int] =
  try Right(in.toInt)
  catch {
    case e: NumberFormatException => Left(in)
  }

result match {
  case Right(x) => s"You passed me the Int: $x, which I will increment. $x + 1 = ${x+1}"
  case Left(x)  => s"You passed me the String: $x"
}
```

```Example 2
def Name(name: String): Either[String, String] =
    {
      
        if (name.isEmpty) 
            // Left child for failure
            Left("There is no name.")
  
        else
            // Right child for success
            Right(name)
    }
```

--- 

**Sources:**
- https://www.baeldung.com/scala/
- https://www.geeksforgeeks.org/scala-either/
- https://www.scala-lang.org/api/2.13.6/scala/util/Either.html