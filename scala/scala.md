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
val firstName = "Jon"
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



* classes
* case class
* case Some? https://stackoverflow.com/questions/49944872/understanding-some-and-option-in-scala
* inheritence
* packaging and sbt


baseDf.withColumn("__hoodie_active", if (op.equals("d")) lit(0) else lit(1))
