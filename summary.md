# Slides 1: **Introduction**

### Why OOP?
  
1. Data Abstraction.
2. Encapsulation. 
3. Information Hiding. 
4. Polymorphism. 
5. Inheritance.
6. Reusability.

### Characteristics of Java 
- Java Is Simple 
- Java Is Object-Oriented 
- Java Is Distributed 
- Java Is Interpreted 
- Java Is Robust 
- Java Is Secure 
- Java Is Architecture-Neutral 
- Java Is Portable 
- Java's Performance 
- Java Is Multithreaded
- Java Is Dynamic

### PROG 0: Welcome to Java
```java 
// This program prints Welcome to Java!
public class Welcome {
    public static void main(String[] args) { 
        System.out.println("Welcome to Java!");
    }
}
```

### DataTypes:
> They are the same as C language except `boolean` instead of `bool`.

### Math Operators:
> They are the same as C language except `Math.pow()`, `Math.sqrt()` and others.

### Relational Operators:
> They are the same as C language.


### Logical Operators:
> They are the same as C language, but keep the XOR operator in mind (`^`).

### Rounding Methods:
> `round()` method works normally on positive numbers.  
> but `-1.5` is rounded to `-1`, **not** `-2`.

### `random()` Method
> returns random number from 0 to less than 1.  
> Thus:  
> `a + (int) random() * b` returns a number from $a$ to $a + b - 1$

### Helpful `String` Methods:
- `length()`
- `charAt(index)`
- `concat(s1)` $\rightarrow$ you can also use `+` operator to concatenate strings.
- `toUpperCase()`
- `toLowerCase()`
- `trim()` $\rightarrow$ trims leading/trailing whitespace.
- `equals(s1)`
- `equalsIgnoreCase(s1)`
- `compareTo(s1)` $\rightarrow$ returns `1` or `0` or `-1` if string is alphanumerically greater, equal to, or smaller than `s1`.  
- `compareToIgnoreCase(s1)`
- `startsWith(prefix)`
- `endsWith(suffix)`
- `indexOf(ch {,fromIndex})` $\rightarrow$ returns `-1` if unmatched

### Declaring Arrays:
```java
// Declaration
double[] myList; // preferred
// or
double myList[]; // not preferred

// Creation
myList = new double[/*arraySize*/];

// Both in a single step
double[] myList = new double[/*arraySize*/];

// Array size is fixed once the array is created
System.out.println("Array size = " + myList.length);

```

---
# Slides 2: **Objects and Classes**

### UML Class Diagram
|Circle|
|-|
radius: double
<u>staticField: type</u>
`+`publicField: type
`-`privateField: type
|_____________________________________|
Circle()
Circle(newRadius: double)
getArea(): double
getPerimeter(): double
setRadius(newRadius: double): void

### UML Object
|<u>circle1: Circle</u>|
|-|
radius = 1.0

### Constructor Example
```java
// no arg constructor
Circle() {
}

// one arg constructor
Circle(double newRadius) {
    radius = newRadius;
}
```

### Single step object creation
```java
Circle myCircle = new Circle();
```

### Static members/methods

> A static member is accessed through the Class, not an object
> ```java
> ClassName.staticMethod(/*param*/);
> ObjectName.nonStaticMethod(/*param*/);
> ```


### Mutability
|Mutable|Immutable|
|:-|:-|
|Its datafields can be changed without creating a new object.| A new object must be created with different datafield values.

### `this` keyword example
```java
public class Circle { 
    private double radius;

    public Circle(double radius) { 
        this.radius = radius;
    }
    public Circle() {
        this(1.0);
    }
}
```

---
# Slides 3: **Thinking in Objects**

## Class Relationships:
- Association
- Aggregation
- Composition
- Inheritance

### **1. Association**:
A general binary relationship that describes an activity between two classes.  
> **Example**: `Student` takes and array of `Course`, `Teacher` teaches an array of `Course`, and `Course` has a `Teacher` and an array of `Students`.

```java
public class Course {
    private Student[] classList;
    private Teacher teacher;

    public void addStudent(Student s) { ... }
    public void setTeacher(Teacher t) { ... }
}

public class Student {
    private Course[] courseList;

    public void addCourse(Course s) { ... }
}

public class Teacher {
    private Course[] courseList;

    public void addCourse(Course c) { ... }
}
```

### **2. Aggregation**:
It models *has-a* relationships, and represents an ownership relation between two objects.
> **Example**: `Student` has an `address`, but multiple `Student`s can have the same `address`.

### **3. Composition**:
It is a special case of Aggregation, but it's one-to-one.

> **Example**: `Student` has a `Name`, and no other `Student` shares the same name.
```java
// Aggregated Class
public class Name {
    ...
}

// Aggregated CLass
public class address {
    ...
}

// Aggregating Class
public class Student {
    private Name name;
    private Address address;

    ...
}
```

```java
// Example on self aggregation
public class Person {
    // The type for the datafield is the class itself
    private Person supervisor;
    private Person[] subordinates;
    ...
}
```

## Wrapper Classes:
- `Boolean`
- `Integer`
- `Character`
- `Long`
- `Short`
- `Float`
- `Byte`
- `Double`

> Note:  
> 1. The wrapper classses do bot have no-arg constructors.
> 2. The instances of all wrapper classes are immutable, i.e., their internal values cannot be changed once the objects are created.


### **The `Integer` Class and the `Double` Class**



**Constructors**

```java
public Integer(int value)

public Integer(String s)

public Double(double value)

public Double(String s)
```

**Constants**
- `MIN_VALUE`: represents min value for `Byte`, `Short`, `Integer`, and `Long`. but represents the min **positive** value for `Float`, and `Double`.

**Conversion Methods**  
> Each numeric wrapper class implements the abstract methods `doubleValue()`, `floatValue()`, `intValue()`, `longValue()`, and `shortValue()` which are defined in the `Number` class, they convert objects to primitive type values.


**Static `valueOf` Methods**
> Each numeric wrapper class has `valueOf(String s)` method, which returns a new object with the passed value
> ```java
> Double doubleObject = Double.valueOf("12.4");
> Integer integerObject = Integer.valueOf("12");
> ```
> Similarly for primitive datatypes, `parseInt(String s)` or `parseDouble(String s)` can be used

### `BigInteger` and `BigDecimal`
```java
BigInteger a = new BigInteger("9223372036854775807");
BigInteger b = new BigInteger("2");
BigInteger c = a.multiply(b); // 9223372036854775807 * 2
System.out.println(c);
```

### `String` Class
> **Note on interned strings**:  
> ```java
> String s1 = "Welcome to Java";
> String s2 = new String("Welcome to Java");
> String s3 = "Welcome to Java";
> ```
> a new object is created if this string is a new unique string, OR if the `new` operator is used.  
>   
> `s1 == s2` is `false`  
> `s1 == s3` is `true`  

> **Matching, Replacing, and Splitting using regular expressions**  
> - `"Java".equals("Java")` is `true`
> - `"Java".matches("Java")` is `true`
> - `"Java is fun".matches("Java.*)` is `true`
> - `"Java is cool".matches("Java.*)` is `true`
>
> *Example 1*
> ```java
> String s = "a+b$#c".replaceAll("[$+#]", "NNN");
> System.out.println(s);
> ```
> *Output*
> ``` 
> aNNNbNNNNNNc
> ```
> *Example 2*
> ```java
> String[] tokens = "Java,C?C#,C++".split("[.,:;?]");
> for (int i = 0; i < tokens.length; i++)
>     System.out.println(tokens[i]);
> ```
> *Output*
> ```
> Java
> C
> C#
> C++
> ```

---
# Slides 4: **Inheritance and Polymorphism**

## Inheritance
### Superclasses and Subclasses
> **Example**:  
> ```java
> public class GeometricObject
> {
>     private String color;
>     private boolean filled;
>     ...
> }
> 
> public class Circle extends GeometricObject {
>     private double radius;
>     ...
> }
> 
> public class Rectangle extends GeometricObject {
>     private double width;
>     private double height;
>     ...
> }
> ```

> **Note**:  
> - Superclass's Constructor is always invoked, the compiler will put `super()` as the first statement in every subclass method if not explicitly added., therefore, all superclasses must have a no-arg constructor
> - `super` refers to the superclass of the class in which `super` appears
> - A subclass inherits all the *public* methods in the superclass, but we can write the subclass to override the inherited method(s) if needed.  
>
> |Overriding|Overloading|
> |:-:|:-:|
> The original method and the overriding method have the same signature, the original method is replaced by the new one.|The parameter type is changed, both methods exist simultaneously

### The `Object` Class

Every class in java is descended from the `java.lang.Object` class, if no inheritance is specified when a class is defined, the superclass of the class is `Object`.
> It is a good practice to override the `toString()` and `equals(Object obj)` methods inherited from `Object` class when defining a new class.

## Polymorphism
**Definition**: It means that the variable of a supertype can refer to the subtype
> **Polymorphism Demo**
> ```java
> public class PolymorhpismDemo {
>     public static void main(String[] args) {
>         m(new GraduateStudent());
>         m(new Student());
>         m(new Person());
>         m(new Object());
>     }
> 
>     // this method can take a parameter of any object type
>     public static void m(Object x) {
>         System.out.println(x.toString());
>     }
> }
> 
> class GraduateStudent extends Student {
> }
> 
> class Student extends Person {
>     public String toString() {
>         return "Student";
>     }
> }
> 
> class Person /*extends Object*/ {
>     public String toString() {
>         return "Person";
>     }
> }
> ```

**Dynamic Binding**:
There may be several implementations of a method in an inheritance chain, the JVM searches for the implementation in the class of the reference object or the nearest superclass in which an implementation of the method is found. This search is performed at runtime.

**Method Matching**: it is done at compile-time, where the compiler selects the implementation of a method to be called based on its signature.

### Casting
```java
Object o = new Student(); // Implicit casting
Student b = o; // Error here
```
The previous code will result in an error because every `Student` is an `Object`, but not every `Object` is a `Student`.  
Explicit casting will be required in this case
```java
Object o = new Student(); // Implicit casting
Student b = (Student) o; // Explicit casting
```

> **Note**  
> Explicit casting must be used when casting an object from a superclass to a subclass. And this type of casting may not always succeed.

### The `instanceof` Operator
```java
Object myObject = new Circle();

... // some lines of code

// Perform casting of myObject is an instance of Circle 
if (myObject instanceof Circle) {
    System.out.println("The circle diameter is " + ((Circle)myObject).getDiameter());
    ...
}
```
### The `protected` Modifier:
**Accessibility Summary**
|Modifier on members in a class|Accessed from the same class|Accessed from the same package|Accessed from a subclass|Accessed from a different package|
|:-:|:-:|:-:|:-:|:-:|
`public`|$\checkmark$|$\checkmark$|$\checkmark$|$\checkmark$
`protected`|$\checkmark$|$\checkmark$|$\checkmark$|-
default|$\checkmark$|$\checkmark$|-|-
`private`|$\checkmark$|-|-|-

> **Note**: A subclass cannot weaken the accessibility when overriding an inherited method

### The `final` Modifier:
> - The `final` class cannot be extended:
> ```java
> final class Math {
>     ...
> }
> ```
> - The `final` variable is a constant:
> ```java
> final static double PI = 3.14159;
> ```
> - The `final` method cannot be overridden by its subclasses.

---
# Slides 5: **Abstract Classes and Interfaces**

## **Abstract Classes**

**Abstract Class**: It is a class that cannot be instantiated, and can be inherited
> **Note**  
> - in UML diagram:  
>   - the `abstract class` name, and `abstract` methods' names are *italicized*
>   - the `protected` modifier is represented with a hash symbol (#)
> - `abstract` methods can only be defined in `abstract` classes
> - The subclass will also be `abstract` unless all the `abstract` methods in all the superclassess are overridden.
> - The superclass of an `abstract` class may be concrete
> - A concrete method may be overridden as `abstract`

`abstract` **method declaration**:
```java
public abstract double getArea(); // semicolon here
// no body
```

## **Interfaces**
> **Note**
> - A class may implement any number of interfaces.
> - In UML diagram, its name is *italicized* and the tag «interface» precedes it.
> - All `interface` methods are implicitly defined as `public abstract`.
> - to use `java.utl.Arrays.sort()`, implement Comparatble `interface` and override `compareTo()` method.

**Example `interface` definition**
```java
public interface Edible {
    // constant declarations
    ...

    // abstract method signatures
    public abstract String howToEat();
    ...
}
```

**Comparable `interface` Implementation**
```java
public class Integer extends Number implements Comparable<Integer> {
    // class body ommitted

    @Override
    public int compareTo(Integer o) {
        // implementation omitted
    }
}
```

**Cloneable `interface`**  
It is an empty `interface` that doesn't contain constants or methods.  
It is used to denote that a class possesses certain desirable properties. A class that implements the `Cloneable interface` is marked Cloneable, and its objects can be cloned using the `clone()` method defined in the Object class.

```java
package java.lang;

public interface Cloneable {
}
```

||Shallow Copy|Deep Copy|
|:-:|:-:|:-:|
Primitive data fields|A new one is created in memory|A new one is created in memory
Object data fields|The reference is copied|A new object is created