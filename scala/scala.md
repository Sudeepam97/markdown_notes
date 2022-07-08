# Introduction
* Scala is statically typed, meaning that the variables types are known or determined at compile time.
* Type inference is available.
* Scala code produces .class files that run over JVM (Java Virtual Machine).
* Java libraries can be used with Scala code.
* Object Oriented and Functional paradigms are supported.
* Use `//` for single line and `/* */` for multi-line comments.
* Naming is mostly done using camel case.




# Hello World
```scala
// filename: learn.scala
object Hello {
    def main(args: Array[String]) = {
        println("Hello, world")
    }
}
```
Description of the above code..

* `main` is the name of a `method` inside a Scala `object` named `Hello`.
* An `object` is similar to a `class`, but we specifically use it when we want a single instance of the class.
* `main` takes an input parameter named `args` that is a `string` array for command line arguments.
* When called, `main` prints "Hello, world"

To run the code...
```sh
scalac learn.scala          # to compile to class files (JVM bytecode)
scala Hello                 # to run the class file
```

Instead of writing the main method ourselves, we can extend a `trait` called `App` which already has a main method defined.

```scala
object Hello extends App {
    println("Hello, world")
}
```



# Data Types

Primitive Types are same as JAVA, but a first word is capitalized.
```
Int
Long
Float
Double
Char
Short
Byte
Boolean
```


# Scala REPL
Scala isn't really a interpreted language, however it offers something called a Scala REPL "Read-Evaluate-Print-Loop", which is a command-line interpreter that can be used as a “playground” to test Scala code. You can type in Scala expressions in the REPL to test them out.

To launch the Scala REPL just type `scala` in a terminal window.

For simple expressions where you don't create variables, REPL automatically stores their results in a variable starting with `res0` (`res1`, `res2`  and so on..).




# Variables
```scala
// immutable variables
val x = 5

// Mutable variables
var x = 5
```

Types are inferred by Scala, but we can also specify the data types ourselves.
```scala
val x: Int = 5
var k: String = "hello"
```

Note that in scala REPL, `val` variables can be redefined (REPL isn't 100% like actual Scala)


# Functional programming basics
```
def square(x: Double): Double = x * x
def sumOfSquares(x: Double, y: Double): Double = square(x) + square(y)

val ans = sumOfSquares(4, 5)

println(ans)
```

The way this program works is that...
* We evaluate (simplify) the function arguments from left to right.
* We replace the body of the function with its definition.
* We repeat this till we are able to reduce the expressions to a value.
 
Hence...
 ```
sumOfSquares(4, 2 + 3)

= sumOfSquares(4, 5)
= square(4) + square(5)
= 4 * 4 + square(5)
= 16 + square(5)
= 16 + 5 * 5
= 16 + 25
= 41
 ```

* This is called the substitution model, as simple as it may seem, we can essentially extend this to implement every algorithm.
* The idea of the model is that all evaluations reduce an expression to a value.
* We can apply this to all expressions, as long as they do not have any side effects (such expressions are called pure functions).

> These are the foundations of functional programming.

It might be possible that ab evaluation does not terminate.
```scala
def x: Int = x
```
This will never terminate since the expression always evaluates to itself.



# Call by value vs Call by name
* Previously we saw that we were reducing the expressions for the function arguments first, and then applying the function. Alternatively, we can also apply the function first to unreduced arguments and then evaluate the expressions after function application. This would be something like...
```
sumOfSquares(4, 2 + 3)

= square(4) + square(2 + 3)
= 4 * 4 + square(2 + 3)
= 16 + (2 + 3) * (2 + 3)
= 16 + 5 * 5
= 16 + 25
= 41

>> Note how we're applying the function first and then evaluating the expressions, unlike before.
```

- reducing and applying = call by value
- applying and reducing = call by name

Both the methods will evaluate an expression to the same value as long as.

1) Reduced expressions are pure functions (no side effects).
2) Both evaluations terminate.

In the example above, we can se that `(2 + 3)` was calculated (evaluated) twice. This is a disadvantage of call by name. In call by value however, such an expression only gets evaluated once. This starts to matter when the expressions are complicated expressions instead of trivial things like addition.

1) In call by value every expression gets evaluated exactly once, which may be an advantage.
2) In call by name, an expression may be evaluated any number of times... even 0 times if a parameter is unused.
```
def test(x: Int, y: Int) = x * x

>> test(2, 3) -> same for both

>> test(2, 1 + 1) -> call by value is faster as we saw before

>> test(2, 3 * 3)

CBV = test(2, 9) = 2 * 9 = 18
CBN = 2 * 3 * 3 = 18

So in this case CBN is faster.
```


# Blocks
Scala expressions can be logically grouped into a block, with a `{}`. For example:
```scala
println({
  val x = 1 + 1
  x + 1     // Result of a block is the result of the final expression
})
```




# Strings
Scala strings are similar to strings from any other language, below are a few things to keep in mind:
```scala
val firstName = "Jhon"
val lastName = "Cena"

// appending strings (method 1)
val name = firstName + " " + lastName

// appending (method 2)
val name = s"$firstName ${lastName}"    // note that {} is just a block for redability

// triple quotes for multi-line strings
val multi = """
                |hello people!
                |what's up?
            """.stripMargin

// The stripMargin method looks for the `|` symbol and strips the indented before it.
```




# IO
Getting Outputs..
```scala
// here's how we usually print stuff
println("Hello, world")

// println adds a newline at the end, so try a print if you don't want that
// This is similar to JAVAs 's.o.p.' and 's.o.p.ln'
print("Hello without newline")

// f-string like printing
val name = "Sudeepam"
println(s"Hello my name is $name")

// We can use java stuff directly, for example to log errors
System.err.println("yikes, an error happened")
```

Taking Inputs..
```scala
// Easiest way is to use readLine method.
// this is not a very commonly used method so needs to be imported.

// Below is an example of how inputs work...
import scala.io.StdIn.readLine

object HelloInteractive extends App {

    print("Enter your first name: ")
    val firstName = readLine()

    print("Enter your last name: ")
    val lastName = readLine()

    println(s"Hello, $firstName $lastName!")

}
```




# IF-ELSE
basic if-else looks like this:
```scala
if (a == b || a+b == 5 ){
    // do something
}
else if (a+b != 5 && a < b){
    // do something else
}
else {
    // do default stuff
}
```

If else returns the output of the conditional block, so we can also have..
```scala
// returns a or b
val output = if (a < b) a else b

// returns Unit() since println is a statement and not an expression
val output = if (a < b) println(a) else println(b)  
```




# FOR Loop
```scala
val nums = List(1,2,3,4,5)

for (n <- nums){
    println(n)
}
```

Scala iterables also has a `foreach` method which works as below..
```scala
people.foreach(println)
```

Here's how we use `for` / `foreach` with maps
```scala
// with for
for ((name, rating) <- movie_ratings){
    println(s"Movie: $name, Rating: $rating")
}

// with foreach
ratings.foreach {
    case(movie, rating) => println(s"key: $movie, value: $rating")
}
// note: `x => y` essentially means the expression x returns the result y
```




# FOR expressions
* In general, when every expression we write returns a value, that style is referred to as expression-oriented programming.
* Conversely, lines of code that don’t return values are called statements, and they are used for their side-effects. For example a for loop line is usually used for iterating through something (hence used for their side-effects).
* In Scala, while a for-loop is used for side effects (such as printing output), a for-expression is used to create new collections from existing collections. They are similar to python's comprehensions.

```scala
val nums = Seq(1,2,3)
val doubledNums = for (n <- nums) yield n * 2
```
* `yield` keyword here states that we want to generate a new collection of 'this' type from the existing collection. We can have as long of an expression as is required after `yield`. Below is an example.
```scala
val names = List("_adam", "_david", "_frank")

val capNames = for (name <- names) yield {
    val nameWithoutUnderscore = name.drop(1)
    val capName = nameWithoutUnderscore.capitalize
    capName
}
// ["Adam", "David", "Frank"]
// note how the last value of the expression is the result.

// Here's a one liner for the same thing
val capNames = for (name <- names) yield name.drop(1).capitalize
```




# match
* `match` is essentially equivalent to the switch statement.
```scala
val monthName = i match {
    case 1  => "January"
    case 2  => "February"
    case 3  => "March"
    case 4  => "April"
    case 5  => "May"
    case 6  => "June"
    case 7  => "July"
    case 8  => "August"
    case 9  => "September"
    case 10 => "October"
    case 11 => "November"
    case 12 => "December"
    case _  => "Invalid month"
}
```




# try-catch and finally
* An example would be enough here:
```scala
try {
    // some code that may fail
} 
catch {
    case foo: FooException => handleFooException(foo)
    case bar: BarException => handleBarException(bar)
    case _: Throwable => println("Got some other kind of Throwable exception")
}
finally {
    // code for closing a database connection or file handle
}
```




# Classes
Here's how you create classes..
```scala
class Person(var firstName: String, var lastName: String = "Unknown") {
    var age = 15     // 'public' access by default
    private val country = "India"   // explicit private access

    def printCountry(){
        println(s"country = $country")
    }
    def printFullName(){
        println(s"$firstName $lastName")
    }
    def ageAfterSomeYears(years: Int): Int = {
        age + years
    }
}

// with this example we also see how methods are written in scala.
// checkout https://stackoverflow.com/questions/944111/when-to-use-the-equals-sign-in-a-scala-method-declaration
// to learn something important about methods in scala
```
To create an instance of this class
```scala
val p = new Person("Sudeepam", "Pandey")
p.age = 23

val ageAfterFive = p.ageAfterSomeYears(years = 5)
println(s"age after 5 years: $ageAfterFive")
```




# Traits
You define a trait when you want to model a basic interface for certain functionality but you don't want to implement any behaviour. The actual behaviour is implemented in the child classes that extend the trait. Trait is esentially like a base class.

As an example, imagine that you want to write some code to model cars.
```scala
trait Cars {
    def startCar(): Unit
    def stopCar(): Unit
}
```
Now this trait states that all Cars should have a method to startCar and stopCar. Additional attributes may also be present. Below is how you extend a trait.
```scala
class ferrari extends Cars {
    def startCar(): Unit = println("ferrari is starting")
    def stopCar(): Unit = println("ferrari is stopping")
}
```
You can also extend a class with multiple traits. This allows us to write a very modular code.
```scala
class a extends b with c with d {
    def funB(): Unit = // some code
    def funC(): Unit = // some code
    def funD(): Unit = // some code
}
// here b, c and d are traits and a is the class that extends them 
```

Traits can also have some methods defined while others are abstract (behaviour not implemented). When required
the pre defined methods can be overriden as well. For example:
```
trait Pet {
    def speak = println("Henlo")     // concrete implementation of a speak method
    def comeToMaster(): Unit         // abstract
}

class Dog(name: String) extends Pet {
    def comeToMaster(): Unit = println("Woo-hoo, I'm coming!")
}

class Cat extends Pet {
    override def speak(): Unit = println("meow")      // override 'speak'
    def comeToMaster(): Unit = println("Not gonna happen.")
}
```

* Scala traits don’t allow constructor parameters. Therefore, we need to use an abstract class whenever a base behavior must have constructor parameters. However, a class can extend only one abstract class whereas it can extend multiple traits.
```
// defining abstract classes
abstract class Pet (name: String) {
    def speak(): Unit = println("Yo")   // concrete implementation
    def comeToMaster(): Unit            // abstract method
}

class Dog(name: String) extends Pet(name){

}

val d = new Dog("Fido")
```




# Scala Collections
Scala collections distinguish between mutable (`scala.collection.mutable`) and immutable (`scala.collection.immutable`) collections. A mutable collection can be updated or extended in place whereas Immutable collections, do not change. Immutable collections do have operations that simulate additions, removals, or updates, but those operations return a new collection and leave the old collection unchanged.

By default, Scala always picks immutable collections. For instance, if you just write `Set` without any prefix or without having imported `Set` from somewhere, you get an immutable set because these are the default bindings imported from the scala package. To get the mutable default versions, you need to explicitly write `collection.mutable.Set`.

Read about the overview of collections and hierarchy here: https://docs.scala-lang.org/overviews/collections/overview.html

| Class / Trait  |               Description                   |                           Overview Doc                                      |
| -------------  |               -----------                   |                           ------------                                      |
| ArrayBuffer    | An indexed, mutable sequence                | https://docs.scala-lang.org/overviews/scala-book/arraybuffer-examples.html  |
| List           | A linear (linked list), immutable sequence  | https://docs.scala-lang.org/overviews/scala-book/list-class.html            |
| Vector         | An indexed, immutable sequence              | https://docs.scala-lang.org/overviews/scala-book/vector-class.html          |
| Map            | The base Map (key/value pairs) class        | https://docs.scala-lang.org/overviews/scala-book/map-class.html             |
| Set            | The base Set class                          | https://docs.scala-lang.org/overviews/scala-book/set-class.html             |

* Map and Set come in both mutable and immutable versions.
* **Note**: `Seq` is a trait and `List` is a class that derives from this trait. The default implementation of a `Seq` is a `List` (see the overview doc linked above) so often you'd see `Seq` being used instead of `List`. Same thing applies to `Map` and `Set`.




# Anonymous functions




* packaging and sbt
* functional programming
* case class
