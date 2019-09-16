# Lecture 3.2 - How Classes Are Organized

### Packages
+ Classes and Objects are organised in packages.

        package progfun.examples
        object Hello {}

    This fully qualified object can be used while compiling or running like `scala progfun.examples.Hello`

+ In order to import a named type from a package we do:

        import progfun.examples.Hello               //named import 
        import progfun.examples.{Hello, Rational}   // imports more than one, named import
        import progfun.examples._                   // imports everything under examples

+ All members of the packages:
- `scala` 
- `java.lang` 
- and the singleton object `scala.Predef` are auto imported.

### Traits
+ In Scala, a class can have only one superclass. It's a single inheritance language.
+ If a class wants to inherit code from more than one supertype we use `traits`.
+ `traits` are declared like an `abstract class` with the keyword  `trait` instead of `abstract class`
```scala
trait Planar {
def height: Int
def width: Int
def surface = height * width
}
```
+ Classes, objects and traits can inherit from at most one class but from many traits.
```scala
class Square extends Shape with Planar with Movable
```
+ Classes inherit code from a trait with the `with` keyword.

+ traits cannot have `val` parameters. But unlike interfaces in Java it can contain concrete methods and fields.

### Scala class hierarchy
![Class hierarchy](https://lh3.googleusercontent.com/Hz5G9eaSlV4yrkxsDZWNNsRpDmarjSQjBUTw7ODeqegy4u03pVYJ36EXOleYEt6t5plCsxxwZ8dCDdNtNBOJJemXnOnRlNDQm-ytc3kxIuEtYU04RE74OhlCMFwDkCM9DEL2efmTbUVg9bW0Ban8dLfOy0Nl2fxeFDtEfE8tezFffz-SnW8NL0ghyq-CqJC-1YIxizaiLoocQdlzfGAgDkTtaOG2Obd_F3wIp5XSjhaN8X6U7Qf7MfYqRF7WRX2MFksFl2Go3Ne-JWzUDUD0h3yy8grua66P6NHERjm2iBk3m7pCwxtehdwELJ8iliHr7C8P8rZ4Uz8AuRwC57GmiOY36MfckDSgvjJVY38J8oVl4WUiRaQEI-HvT9p0Soqq33xc4zAZ5M8F1G8nnVufJwbaY9l7fSOM5f3P5XVb6UbzhaZqno5yZjYm44j6scIzII3txaIYB7fVX4Uu7wakPXEOj_M4IWHK6hvuiZ95aVHqCY339JbIHx8sfyvQ63-9FfVgA35MI1gbpdhSbPHcw7RCeU6tnB1TH3Dnog7MGXH8p_Om95lItqDV-Ah5uZAnW8gNmO29FH4ljDwJOSEKL4o3GBBS_zO4fTWMKCOh_DfDfAy3FahovYKTRYpEpYpDyEt8Nt8iLXZFpvAB3EWerFv6ICMiuRlnbO7N3TpwBhNjCcNyBm9JGw=w1347-h782-no)
+ `Scala.Any` is at the top of scala class hierarchy and is the base type of all scala types. It is also the base type that defines universal methods like `toString`, `equals`, `hashCode`, `==`, `!=`, etc
+ `Scala.AnyVal` is a subclass of `Scala.Any` and is the base class of all primitive types like `Byte`, `Int`, `Double`, etc
+ `Scala.AnyRef` is a base type of all reference types. Alias of `java.lang.Object`. `scala.Iterable`, `scala.Seq`, `scala.List` are base classes of `scala.AnyRef` but they also implement the trait `Scala.ScalaObject`

### Nothing type
+ `Scala.Nothing` is at the bottom of Scala's type hierarchy. It is a subtype of every other type. There is no value of type `Nothing`
+ Used to signal abnormal termination. If sometimes a function throws an exception or terminates unexpectedly, it's return type is of type `Nothing`.
+ Used as an element type of empty collections.
+ An expression `throw exp` returns type `Nothing`

### Null type
+ `Scala.Null` is the subtype of every reference type.
+ Every reference class type also has `null` as a value.
+ The type of `null` is `Null`
+ `Null` is a subtype of every class that inherits from `java.lang.Object`.
+ It is incompatible with subtypes of `AnyVal`

        val x = null
        val y: String = x
        val z: Int = null       // type mismatch

+ `if (true) 1 else false`. The type of this expression is `AnyVal`. Looking at the hierarchy, the common super type of `Int` and `Boolean` is `AnyVal`.
