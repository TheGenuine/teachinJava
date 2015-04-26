### Table of content
1. Introduction 
2. Data structures
3. Conditionals
4. Loops
5. Functions/Methods
6. Classes/objects
7. Inheritance
8. Abstract classes
9. Interfaces
10. Exceptions
11. Packages

****

## 2. Data structures
#### Datatypes

The first thing I want to talk about are data types or data structures. Java has two types of data structures, **primitives** and **object/reference** data types. 

**Primitives**  

	int    (e.g. 123) 
	short  () 
	double (e.g. 17.2)  
	float  (e.g. 3.141657943)  
	long   (e.g. 12345678901234)  
	char   (e.g. 'a')
	byte   (e.g. )
	boolean (true/false)

**Object data classes**  

	String
	Boolean
	Integer
	Double
	Long
	Float
	BigInt

Even if primitives and data classes have the same name, they are **not** the same. The main difference is that you cannot call methods/functions on a primitive because they are no classes or objects. They are as the same says very primitive and do not have any further functionality. Additional functions like `toString()` are contributed by Object data classes which are just classes like every any other. 

**Changing datatypes**
Changing the datatype of a variable is not possible. However, taking a variable as input when creating another variable with a different data type is possible. But not all content types are compatible with each other.

Numbers are all transferable into each other.  
`int -> double` (additional precision will be added by appending a 0 `e.g. 12 -> 12.0`)
the same for `int -> float`

If numbers with a higher precision are transferred into numbers with lower precision  
`e.g. double -> int` everything behind the comma will simply be cut off, no round up or down, just cut off.

When creating a char from an int or any other numerical datatype you will end up with the equivalent character the given number. Always depending on the encoding you use.  (for UTF-8 see [Wikipedia](http://en.wikipedia.org/wiki/UTF-8#Codepage_layout))

## 3. Variables

	private static int sum = 15;

<table>
<tr>
	<td>private</td> 
	<td>visibility, e.g. private, public, protected</td>
</tr>
<tr>
	<td>static</td>
	<td>modifier</td>
</tr>
<tr>
	<td>int</td>
	<td>datatype,  once defined cannot be changed</td>
</tr>
<tr>
	<td>sum</td>
	<td>the variables name</td>
</tr>
<tr>
	<td>= 15</td>
	<td>initial value</td>
</tr>
</table>	

#### Visibility
Only necessary on class level, inside a method any variable is private to that method.

<table>
<tr>
	<td>private</td>
	<td>accessible only from within this class or inheriting classes</td>
</tr>
<tr>
	<td>public</td>
	<td>accessible AND changeable from everywhere</td>
</tr>
<tr>
	<td>protected</td>
	<td>visible and accessible only from classes within the same package</td>
</tr>
</table>	

#### Modifiers
<table>
<tr>
	<td>static</td>
	<td>variable is static within this class, therefore it can be used in static methods without an instance of this class</td>
</tr>
<tr>
	<td>final</td>
	<td>the variables value cannot be changed</td>
</tr>
</table>	

## 6. Classes/Objects
**Defining a class:**  
	
	public class MyClass {
	
	}

<table>
<tr>
	<td>public</td> 
	<td>visibility</td>
</tr>
<tr>
	<td>class</td>
	<td>keyword 'class' to indicate that we want to define a class</td>
</tr>
<tr>
	<td>MyClass</td>
	<td>class name, convention: starts with an upper case letter, written in camelcasing</td>
</tr>
</table>  
  
if a class visibility is 'public' you can only define 1 class per file!  

## Inside a class  

3 things can be defined in a class: 
 
1. construtors  
2. variables  
3. methods  
  
#### 1. Constructors
... are required to instanciate a class. Every class has an invisible default constructor.  
The default constructor takes no arguments and does nothing but creating an instance of that class.
  
If you want to give a class something on the way when creating an instance, you can implement your own custom constructor:

	public MyClass(String name) {
	
	}
	
1. **public**: visibility, should be 'public' if you want to use it outside of this class
2. **MyClass**: the name of the constructor, has to be the same as the class name (with all the capitalisations). **No convention, thats how it is required by java**
3. **String name**: parameters, like method params

Constructors are an exception as they do not have an explicit return type (like methods), because their return type is always the class type itself.

You can have as many constructors as you want, as long as they have different *signatures*. (different parameters). Every call to a constructor creates a new instance of that class, they are no substitute for methods.

**Using the default constructor:**  

MyClass.java  

	public class MyClass {

	}

Main.java  
  
	public class Main {
    	
    	public static void main(String[] args) {
    		MyClass newObject = new MyClass();	
    	}
    }

**Using a custom constructor:**  

MyClass.java  

	public class MyClass {
    		
		private String name;
	
		public MyClass(Stringname) {
			this.name = name;
		}
	}

Main.java  
  
	public class Main {
    	
    	public static void main(String[] args) {
    		MyClass newObject = new MyClass("Peter");  
    	}
    }

## 7. Inheritance

	public class Mylass extends MyOtherClass {
		// ...
	}

You will inherit/have access to all methods and public variables defined in the parent class.
> You can only inherit from 1 class!

When instanciating a class that inherits from another class, only the constructor of the subclass gets executed. If you want to include the parent constructor in the execution you can call the parent constructor with `super()`.

	public MyClass(String name) {
		super(name);
		this.name = name;
	}

### Override

When inheriting from a class it is possible to override methods of the parent class. 
e.g. if your subclass a special use case for a method.

Nameable.java

	public class Nameable {
		// ...
		public String getSurname() {
			return this.surname;
		}
	}

MyClass.java

	public class MyClass extends Nameable {
		// ...
		@Override
		public String getSurname() {
			return this.surname + " " + this.surname2;
		}
	}

When overwriting a method the parent method is just hidden. To call the parent version of the method use `super`.

	@Override
	public String getSurname() {
		return super.getSurname() + " " + this.surname2;
	}

## 8. Abstract classes

	public abstract class MyAbstractClass {
		// ...
	}

With the keyword `abstract` you can define a class as abstract. Abstract classes cannot be instantiated. Their static parts can be used as normal, when trying to create an object instance from it the compiler will complain.

So what are abstract classes good for?
For one they are very suitable to serve as a kind of "base class" other classes can inherit from. It might implement a quite abstract concept and it is for the subclasses to implement specific use cases.

Vehicle.java

	public abstract class Vehicle {

	    public final int wheels;
	    private final String make;
	    
	    public Vehicle(String make, int wheels) {
	        this.make = make;
	        this.wheels = wheels;
	    }
	    
	    public void brumm() {
	        System.out.println("Brummmm");
	    }
	}
Truck.java

	public class Truck extends Vehicle {
	    private String make;
	    public Truck(String make, int wheels) {
	        super(make, wheels);
	        this.make = make;
	    }
	    
	    public void something() {
	        super.brumm(); // calling brumm() of the parent class
	        brumm(); // calling the local version
	    }
	    
	    @Override
	    public void brumm() {
	
	    }
	}

## 9. Interfaces

	public interface MyInterface {
	
		public String callMeNames(String name);
	}

Interfaces are like abstract classes as you cannot instantiate them but there are some more differences.

> - Interfaces only define method signatures, they do **not** implement any method.  
> - A class can implement more than 1 interface 

To implement an interface you "Override" its methods.

	public class MyClass implements MyInterface {
	
		@Override
		public String callMeNames(String name) {
			// ...
		}
	}

> You have to "Override" every method declared in the interface whether you actually implement the method or not.

## 10. Exceptions

If something goes wrong an exception is thrown. In Java a method has to declare if and what kind of exception it may throw.

	public String readConfigFile(String filePath) throws IOException {
		// ...
	}

If you are using a method that might throw an exception you can do 2 things:

1. Handle the exception in a try/catch block
2. Hand the exception up the stack by declaring your method the throw this kind of exception.

**1. Try/catch**

	try {
		readConfigFile("/path/to/the/file.config");
	} catch(IOException e){
        System.err.println(e.getMessage());
	}
You can catch more than one exception type with a try/catch block:

	try {
		readConfigFile("/path/to/the/file.config");
	} catch(IOException e){
        System.err.println(e.getMessage());
	} catch(InterruptedException e) {
		// do something else
	}

**2. Hand the exception up the stack**

If you don't want to handle the exception directly inside one method you can pass the exception on to the calling method.

	public void setupSystem() throws IOException {
		readConfigFile("/path/to/the/file.config");
	}  
In this case the calling method has to handle the exception or pass it on as well.
Exceptions that are not handled anywhere will stop the execution of your program and "crash it". Crashing is not always a bad thing, in some circumstances it might be good to stop application.

## 11. Packages

Packages are a way to group and organise your code. 

	package teachingJava.interfaces;

In variables and methods we encountered `protected` as visibility option.  
