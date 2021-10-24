# OOP in PHP

 - What is OOP
 - Classes and Objects
 - Access Modifiers
 - Constructor
 - Destructor 
 - Inheritance
 - Class Constants
 - Abstract Classes
 - Interfaces
 - Polymorphism
 - Traits
 - Static Methods and Properties
 - Magic Methods
 - Working with Objects
 - Namespaces
 - Exception Handling
 - Autoloading and Composer


##  What is OOP?

From PHP5, you can also write PHP code in an object-oriented style.
OOP stands for Object-Oriented Programming.

Procedural programming is about writing procedures or functions that perform operations on the data, while object-oriented programming is about creating objects that contain both data and functions.

Object-oriented programming has several advantages over procedural programming:
-   OOP is faster and easier to execute
-   OOP provides a clear structure for the programs
-   OOP helps to keep the PHP code DRY "Don't Repeat Yourself", and makes the code easier to maintain, modify and debug
-   OOP makes it possible to create full reusable applications with less code and shorter development time

**Tip:** The "Don't Repeat Yourself" (DRY) principle is about reducing the repetition of code. You should extract out the codes that are common for the application, and place them at a single place and reuse them instead of repeating it.

----------

### PHP - What are Classes and Objects?

Classes and objects are the two main aspects of object-oriented programming.
Look at the following illustration to see the difference between class and objects:

So, a class is a template for objects, and an object is an instance of a class.

When the individual objects are created, they inherit all the properties and behaviors from the class, but each object will have different values for the properties.

![enter image description here](https://raw.githubusercontent.com/gitmag-group-admin/oop_php/main/01.jpg)

## PHP OOP - Classes and Objects

A class is a template for objects, and an object is an instance of class.

### OOP Case

Let's assume we have a class named Fruit. A Fruit can have properties like name, color, weight, etc. We can define variables like $name, $color, and $weight to hold the values of these properties.

When the individual objects (apple, banana, etc.) are created, they inherit all the properties and behaviors from the class, but each object will have different values for the properties.

### Define a Class
A class is defined by using the `class` keyword, followed by the name of the class and a pair of curly braces ({}). All its properties and methods go inside the braces:

```php
class Car{  
	// code goes here...  
}
```

Below we declare a class named Fruit consisting of two properties ($brand and $color) and two methods decrease_speed() and increase_speed():

```php
class Car{  
	// Properties  
	public $brand;  
	public $color;  
  
	// Methods  
	public function decrease_speed() {  
		echo "decrease speed";  
	}  
	public function increase_speed() {  
		echo"increase speed";  
	}  
}
```

> **Note:** In a class, variables are called properties and functions are called methods!

### Define Objects

Classes are nothing without objects! We can create multiple objects from a class. Each object has all the properties and methods defined in the class, but they will have different property values.
Objects of a class is created using the `new` keyword.
In the example below, $bmw instance of the class Car:

```php
$bmw = new Car();  

$bmw->brand = 'bmw';  
$bmw->color = 'red';  
  
echo $bmw->brand;  
echo "\n";  
echo $bmw->color;
echo "\n";

$bmw->decrease_speed();
$bmw->increase_speed();
```

### The $this Keyword
The $this keyword refers to the current object, and is only available inside methods.
Look at the following example:

```php
class Car{  
	public $brand;  
}  

$benz = new Car();
```

Inside the class (by adding a set_name() method and use $this):

```php
class Car{  
	public $brand;  
	
	public function set_brand($brand) {  
		$this->brand = $brand;  
	}  
}  

$bmw = new Car();  
$bmw->set_brand("bmw");  
  
echo $bmw->brand;
```

2. Outside the class (by directly changing the property value):

```php
class Car{  
	public $brand;  
}  

$bmw = new Car();  
$bmw->brand = "benz";  
  
echo $bmw->brand;
```

### Chaining Methods

```php
class Calculate {
	public $total = 0;

	public function get_total() {
		return $this->total;
	}

	public function addition($number) {
		$this->total += $number;
	}
	
	public function submission($number) {
		$this->total -= $number;
	}
}

$calculate = new Calculate();
$calculate->addition(200);
$calculate->addition(400);
$calculate->submission(350);
$calculate->addition(500);
echo $calculate->get_total();
```
This code is quite verbose. It would be more concise and expressive if you can write these statements using a single statement like this:

```php
class Calculate {
	public $total = 0;

	public function get_total() {
		return $this->total;
	}

	public function addition($number) {
		$this->total += $number;
		return $this;
	}
	
	public function submission($number) {
		$this->total -= $number;
		return $this;
	}
}

$calculate = new Calculate();
echo $calculate->addition(200)
	->addition(400)
	->submission(350)
	->addition(500)
	->get_total();
```

### instanceof

You can use the `instanceof` keyword to check if an object belongs to a specific class:

```php
$bmw = new Car();  
var_dump($bmw instanceof Car);
```

## Access Modifiers

### Introduction to PHP access modifiers
In the objects and classes tutorial, you have learned about how to use the `public` access modifier with properties and methods.

In fact, PHP has three access modifiers: `public`, `private`, and `protected`. In this tutorial, you’ll focus on the `public` and `private` access modifiers.

-   The `public` access modifier allows you to access properties and methods from both inside and outside of the class.
-   The `private` access modifier prevents you from accessing properties and methods from the outside of the class.

### The public access modifier
When you place the `public` keyword in front of a property or a method, the property or method becomes public. It means that you can access the property and method from both inside and outside of the class.

The following example illustrates the `public` access modifier:

```php
class Customer {
	public $name;

	public function get_name() {
		return $this->name;
	}
}
```
In this example, the `Customer` class has a `public` property (`$name`) and `public` method (`get_name()`). And you can access the property and method from both inside and outside of the class. For example:

```php
$customer = new Customer();
$customer->name = 'Sohrab';
echo $customer->get_name(); // Sohrab
```
How it works.

### The private access modifier
To prevent access to properties and methods from outside of the class, you use the `private` access modifier. The following example changes `$name` property of the `Customer` class from `public` to `private`:

```php
class Customer {
	private $name;
}
```

If you attempt to access the `$name` property from the outside of the class, you’ll get an error. For example:

```php
$customer = new Customer();
$customer->name = 'Sohrab';
```

Error:
`Fatal error: Uncaught Error: Cannot access private property Customer::$name`

So how do you access a `private` property?

To manipulate the value of a private property, you need to define a public method and use the method to manage the private property.

Typically, you need to define two kinds of public methods to manage a private property:

-   A getter returns the value of the private property.
-   A setter sets a new value for the private property.

By convention, the getter and setter have the following name:

```php
get_property
set_property
```

The following `Customer` class defines the getter (`get_name`) and setter(`set_name)` to get and set the value of the `$name` property:

```php
class Customer {
	private $name;

	public function set_name($name) {
		$this->name = $name;
	}

	public function get_name() {
		return $this->name;
	}
}
```

And the following shows how to use the `set_name()` and `get_name()` methods to set and get the value of the `$name` property:

```php
$customer = new Customer();
$customer->set_name('Sohrab');
echo $customer->get_name();
```

### Why do you need private property?
It may be quicker to use the `public` access modifier for properties instead of using a private property with the public getter/setter.

However, by using the `private` the property, you can prevent direct access to the property from the outside of the class.

In addition, the getter/setter methods ensure that the only way to access the property is through these methods. And the getter/setter methods can provide custom logic to manipulate the property value.

For example, if you want the value of the `$name` property to be not blank, you can add the validation logic to the `set_name()` method as follows:

```php

class Customer {
	private $name;

	public function set_name($name) {
		$name = trim($name);

		if ($name == '') {
			return false;
		}
		$this->name = $name;
		return true;
	}

	public function get_name() {
		return $this->name;
	}
}

$customer = new Customer();
$customer->set_name(' Sohrab ');
echo $customer->get_name();
```

In the `setName()` method:

-   First, remove all leading and trailing whitespace using the `trim()` function.
-   Second, return false if the `$name` argument is blank. Otherwise, assign it to the `$name` property and return `true`.


**Encapsulation** is one of the fundamentals of OOP (object-oriented programming). It refers to the bundling of data with the methods that operate on that data. Encapsulation is used to hide the values or state of a structured data object inside a class, preventing unauthorized parties’ direct access to them. Publicly accessible methods are generally provided in the class (so-called getters and setters) to access the values, and other client classes call these methods to retrieve and modify the values within the object

![enter image description here](https://raw.githubusercontent.com/gitmag-group-admin/oop_php/main/04.jpg)

## Constructor

### The __construct Function

A constructor allows you to initialize an object's properties upon creation of the object.

If you create a `__construct()` function, PHP will automatically call this function when you create an object from a class.

Notice that the construct function starts with two underscores (__)!

We see in the example below, that using a constructor saves us from calling the set_name() method which reduces the amount of code:

```php
class Car{  
	private $brand;  
  
	public function set_brand($brand) {  
		$this->brand = $brand;  
	}  
	public function get_brand() {  
		return $this->brand;  
	}  
}  
  
$benz = new  Car();
$benz->set_brand('benz');
echo $benz->get_brand();
```

with `constructor`:

```php
class Car {  
	private $brand;  
	private $color;  
	  
	public function __construct($brand, $color)
	{  
		$this->brand= $brand;  
		$this->color = $color;  
	}  
	public function get_brand() {  
		return $this->brand;  
	}  
	public function get_color() {  
		return $this->color;  
	}  
}  
  
$car = new Car("Audi", "red");  
echo $car->get_brand();  
echo "\n";  
echo $car->get_color();
```

## Destructor 

### The __destruct Function

A destructor is called when the object is destructed or the script is stopped or exited.

If you create a `__destruct()` function, PHP will automatically call this function at the end of the script.

Notice that the destruct function starts with two underscores (__)!

The example below has a __construct() function that is automatically called when you create an object from a class, and a __destruct() function that is automatically called at the end of the script:

```php
class Car {  
private $brand;  
	private $color;  
	  
	public function __construct($brand, $color)
	{  
		$this->brand= $brand;  
		$this->color = $color;  
	}  
	
	public function get_brand() {  
		return $this->brand;  
	}  
	
	public function get_color() {  
		return $this->color;  
	}  

	function __destruct() {  
		echo "\nThe car is {$this->brand}.\n";  
	}  
}  
  
$car = new Car("barnd");
echo $benz->get_name();
```

> **Tip:** As constructors and destructors helps reducing the amount of code, they are very useful!

## Inheritance

### What is Inheritance?

Inheritance in OOP = When a class derives from another class.
The child class will inherit all the public and protected properties and methods from the parent class. In addition, it can have its own properties and methods.

![enter image description here](https://raw.githubusercontent.com/gitmag-group-admin/oop_php/main/05.png)

An inherited class is defined by using the `extends` keyword.
Let's look at an example:

```php
class Car{  
	private $brand;  
	private $color; 
	 
	public function set_brand($brand) {  
		$this->brand = $brand;  
	}  
	
	public function set_color($color) {  
		$this->color = $color;  
	}  
	
	public function get_brand() {  
		return $this->brand;  
	}  
	
	public function get_color() {  
		return $this->color;  
	}  
}  
  
// Strawberry is inherited from Fruit  
class Bmw extends Car {  
	private $model; 
	
	public function set_model($model) {  
		$this->model = $model;  
	}  
	public function get_model() {  
		return $this->model;  
	}  
}  

$bmw = new Bmw();  

$bmw->set_model("x6");
echo $bmw->get_model();  
echo "\n";
$bmw->set_name("bmw");
$bmw->set_brand("red");
echo $bmw->get_brand();
```

#### How to Call the Parent Constructor
in this tutorial, you’ll learn how to call the parent constructor from the constructor of the child class.
```php
class Car{  
	private $brand;  
	private $color; 
	 
	public function __construct($brand, $color) {  
		$this->brand = $brand;  
		$this->color = $color;  
	}  
	
	public function get_brand() {  
		return $this->brand;  
	}  
	
	public function get_color() {  
		return $this->color;  
	}  
}  
  
// Strawberry is inherited from Fruit  
class Bmw extends Car {  
	private $model; 
	
	public function set_model($model) {  
		$this->model = $model;  
	}  
	
	public function get_model() {  
		return $this->model;  
	}  
}  

$bmw = new Bmw("bmw", "red");  
$bmw->set_model("x6");
echo $bmw->get_model();  
echo "\n";
echo $bmw->get_brand();
```

#### Define a constructor in the child class
A child class can have its own constructor. For example, you can add a constructor to the `Bmw` class as follows:

```php
class Car{  
	private $brand;  
	private $color; 
	 
	public function __construct($brand, $color) {  
		$this->brand = $brand;  
		$this->color = $color;  
	}  
	
	public function get_brand() {  
		return $this->brand;  
	}  
	
	public function get_color() {  
		return $this->color;  
	}  
}  
  
// Strawberry is inherited from Fruit  
class Bmw extends Car {  
	private $model; 

	public function __construct($brand, $color, $model) {  
		parent::__construct($brand, $color);
		$this->brand = $brand;  
	} 
	
	public function get_model() {  
		return $this->model;  
	}  
}  

$bmw = new Bmw("bmw", "red", "x6");  

echo $bmw->get_model();  
echo "\n";
echo $bmw->get_brand();
echo $bmw->get_name();
```
-   The constructor of the child class doesn’t automatically call the constructor of its parent class.
-   Use `parent::__construct(arguments)` to call the parent constructor from the constructor in the child class.

### Inheritance and the Protected Access Modifier

The `protected` properties and methods can be accessed from the inside of the class and any class that extends the class.

Like the `private` and `public` access modifier, you prefix the property name with the protected keyword to define a protected property:

### protected property example

```php
class Customer {
	private $name;
	
	public function __construct($name){
		$this->name = $name;
	}
}

class VIP extends Customer {
	public function getFormattedName(){
		return ucwords($this->name);
	}
}


$sohrab = new VIP('sohrab');
echo $sohrab->getFormattedName();
```
Since `$name` property is private, you can only access it within the `Customer` class. To allow the child class to access the `$name` property, you can change it to a protected property like this:

```php
class Customer {
	protected $name;
	
	public function __construct($name){
		$this->name = $name;
	}
}

class VIP extends Customer {
	public function getFormattedName(){
		return ucwords($this->name);
	}
}


$sohrab = new VIP('sohrab');
echo $sohrab->getFormattedName();
```

### protected method example

```php
class Customer {
	protected $name;

	public function __construct($name){
		$this->name = $name;
	}

	protected function format(){
		return ucwords($this->name);
	}

	public function getName(){
		return $this->format($this->name);
	}
}

class VIP extends Customer{
	protected function format(){
		return strtoupper($this->name);
	}
}

$sohrab = new Customer('sohrab azinfar');
echo $sohrab->getName(); // sohrab azinfar

echo "\n";

$hossein = new VIP('hossein mohammadi');
echo $hossein->getName(); // HOSSEIN MOHAMMADI
```

Use `protected` properties and methods can only be accessed within the class and in any child classes of the class.

### Overriding Inherited Methods

To override a method, you redefine that method in the child class with the same name, parameters, and return type.

The method in the parent class is called **overridden method,** while the method in the child class is known as the **overriding method**. The code in the overriding method overrides (or replaces) the code in the overridden method.

PHP will decide which method (overridden or overriding method) to call based on the object used to invoke the method.

-   If an object of the parent class invokes the method, PHP will execute the overridden method.
-   But if an object of the child class invokes the method, PHP will execute the overriding method.

Let’s take an example to understand method overriding better.

```php
class Robot {
	public function greet(){
		return 'Hello!';
	}
}

class Android extends Robot {	
}

$android = new Android();
echo $android->greet(); // Hello!

```

Sometimes, you want to completely replace the method’s behavior of the parent class with a new one. In this case, you need to override the method of the parent class.

To override a method, you redefine the method in the parent class again in the child class but use a different logic.

```php
class Robot{
	public function greet(){
		return 'Hello!';
	}
}

class Android extends Robot{
	public function greet(){
		return 'Hi';
	}
}

$robot = new Robot();
echo $robot->greet(); // Hello

$android = new Android();
echo $android->greet(); // Hi!
```

### Call the overridden method in the overriding method

When you override a method, you will have two versions of the same method: one in the parent class and the other in the child class.

If you call the method of the parent class in the method in the child class, you cannot use $this keyword like this:

```php
class Robot{
	public function greet(){
		return 'Hello!';
	}
}

class Android extends Robot{
	public function greet(){
		$greeting = $this->greet();
		return $greeting . ' from Android.';
	}
}

$android = new Android();
echo $android->greet();
```

To call the `greet()` method of the `Robot` class, you need to use the `parent` with the scope resolution operator `(::`) like the following:

```php
class Robot{
	public function greet(){
		return 'Hello!';
	}
}

class Android extends Robot{
	public function greet(){
		$greeting = parent::greet();
		return $greeting . ' from Android.';
	}
}

$android = new Android();
echo $android->greet();
```

### The final method

The `final` keyword can be used to prevent class inheritance or to prevent method overriding.
The following example shows how to prevent class inheritance:

```php
class Robot{
	public function greet(){
		return 'Hello!';
	}

	final public function id(){
		return uniqid();
	}
}

class Android extends Robot{
	public function greet(){
		$greeting = parent::greet();
		return $greeting . ' from Andoid.';
	}

	public function id(){
		return uniqid('Android-');
	}
}
```

## Class Constants
Constants cannot be changed once it is declared.
Class constants can be useful if you need to define some constant data within a class.
A class constant is declared inside a class with the `const` keyword.
Class constants are case-sensitive. However, it is recommended to name the constants in all uppercase letters.
We can access a constant from outside the class by using the class name followed by the scope resolution operator (`::`) followed by the constant name, like here:

```php
class Bmw{  
	const DATABASE_NAME = "test";  
}  
  
echo Bmw::DATABASE_NAME ;
```

Or, we can access a constant from inside the class by using the `self` keyword followed by the scope resolution operator (`::`) followed by the constant name, like here:

```php
class Database{  
	const DATABASE_NAME = "test";  

	public function connect() {  
		echo "connected to " . self::DATABASE_NAME . "database";  
	}
}  
```

## Abstract Classes

### What are Abstract Classes and Methods?

Abstract classes and methods are when the parent class has a named method, but need its child class(es) to fill out the tasks.
An abstract class is a class that contains at least one abstract method. An abstract method is a method that is declared, but not implemented in the code.
An abstract class or method is defined with the `abstract` keyword:

```php
abstract class ParentClass {  
	abstract public function someMethod1();  
	abstract public function someMethod2($name, $color);  
	abstract public function someMethod3() : string;  
}
```

When inheriting from an abstract class, the child class method must be defined with the same name, and the same or a less restricted access modifier. So, if the abstract method is defined as protected, the child class method must be defined as either protected or public, but not private. Also, the type and number of required arguments must be the same. However, the child classes may have optional arguments in addition.

So, when a child class is inherited from an abstract class, we have the following rules:
-   The child class method must be defined with the same name and it redeclares the parent abstract method
-   The child class method must be defined with the same or a less restricted access modifier
-   The number of required arguments must be the same. However, the child class may have optional arguments in addition

Let's look at an example:

```php
// Parent class  
abstract class Car {  
	protected $brand; 
	protected $color;  
	
	public function __construct($brand, $color) {  
		$this->barnd = $brand; 
		$this->color = $color;  
	}  
	
	abstract public function intro() : string;  
}  
  
// Child classes  
class Audi extends Car {  
	public function intro() : string {  
		return "Choose German quality! I'm an $this->brand!\n";  
	}  
}  
  
class Volvo extends Car {  
	public function intro() : string {  
	return "Proud to be Swedish! I'm a $this->brand!\n";  
	}  
}  
  
class Citroen extends Car {  
	public function intro() : string {  
		return "French extravagance! I'm a $this->brand!\n";  
	}  
}  
  
// Create objects from the child classes  
$audi = new audi("audi", "white");  
echo $audi->intro();  ;  
  
$volvo = new volvo("Volvo", "red");  
echo $volvo->intro();    
  
$citroen = new citroen("Citroen", "green");  
echo $citroen->intro();
```

The Audi, Volvo, and Citroen classes are inherited from the Car class. This means that the Audi, Volvo, and Citroen classes can use the public $name property as well as the public __construct() method from the Car class because of inheritance.

But, intro() is an abstract method that should be defined in all the child classes and they should return a string.

### More Abstract Class Examples
Let's look at another example where the abstract method has an argument, and the child class has two optional arguments that are not defined in the parent's abstract method:

```php
abstract class Database {
	abstract public function connect($name);
}

class Mysql extends Database {
	protected function connect($name) {
		echo "connected to $name database in Mysql.\n";
	}
}

class Sqlite extends Database {
	protected function connect($name) {
		echo "connected to $name database in Sqlite.\n";
	}
}

class SqlServer extends Database {
	protected function connect($name) {
		echo "connected to $name database in SqlServer.\n";
	}
}

$mysql = new Mysql();
$mysql->connect('database_1');

$sqlite = new Sqlite();
$sqlite->connect('database_2');

$sql_server = new SqlServer();
$sql_server->connect('database_3');
```

## Interfaces

### What are Interfaces?

Interfaces allow you to specify what methods a class should implement.
Interfaces make it easy to use a variety of different classes in the same way. When one or more classes use the same interface, it is referred to as "polymorphism".
Interfaces are declared with the `interface` keyword:

```php
interface InterfaceName {  
	public function someMethod1();  
	public function someMethod2($name, $color);  
	public function someMethod3() : string;  
}
```

### Using Interfaces
To implement an interface, a class must use the `implements` keyword.
A class that implements an interface must implement **all** of the interface's methods.

```php
interface Database {
	abstract public function connect($name);
}

class Mysql implements Database {
	protected function connect($name) {
		echo "connected to $name database in Mysql.\n";
	}
}

class Sqlite implements Database {
	protected function connect($name) {
		echo "connected to $name database in Sqlite.\n";
	}
}

class SqlServer implements Database {
	protected function connect($name) {
		echo "connected to $name database in SqlServer.\n";
	}
}

$mysql = new Mysql();
$mysql->connect('database_1');

$sqlite = new Sqlite();
$sqlite->connect('database_2');

$sql_server = new SqlServer();
$sql_server->connect('database_3');
```

Like a class, an interface can extend another interface using the `extends` keyword. The following example shows how the `Document` interface extends the `Database` interface:
```php
interface Animal{
	public function eat();
	public function sleep();
}

interface Cats extends Animal{
	public function hunt();
}
```

## Polymorphism

Polymorphism is a Greek word that literally means many forms. In object-oriented programming, polymorphism is closely related to inheritance.

Polymorphism allows objects of different classes to respond differently based on the same message.

To implement polymorphism in PHP, you can use either abstract classes or interfaces.

Polymorphism helps you create a generic framework that takes the different object types that share the same interface.

Later, when you add a new object type to the system, you don’t need to change the framework to accommodate the new object type as long as it implements the same interface.

By using polymorphism, you can reduce coupling and increase code reusability.

### PHP polymorphism using an abstract class
```php
// Absstract definition  
abstract class Animal {  
	public function makeSound(): void;  
}  
  
// Class definitions  
class Cat extends Animal {  
	public function makeSound() {  
		echo "Meow\n";  
	}  
}  
  
class Dog extends Animal {  
	public function makeSound() {  
		echo "Bark\n";  
	}  
}  
  
class Mouse extends Animal {  
	public function makeSound() {  
		echo " Squeak\n";  
	}  
}  
  
// Create a list of animals  
$cat = new Cat();  
$dog = new Dog();  
$mouse = new Mouse();  
$animals = array($cat, $dog, $mouse);  
  
// Tell the animals to make a sound  
foreach($animals as $animal) {  
	$animal->makeSound();  
}
```

### PHP polymorphism using an interface
The following example is the same as the above except that it uses an interface instead of an abstract class.
```php
// Interface definition  
interface Animal {  
	public function makeSound(): void;  
}  
  
// Class definitions  
class Cat implements Animal {  
	public function makeSound() {  
		echo "Meow\n";  
	}  
}  
  
class Dog implements Animal {  
	public function makeSound() {  
		echo "Bark\n";  
	}  
}  
  
class Mouse implements Animal {  
	public function makeSound() {  
		echo " Squeak\n";  
	}  
}  
  
// Create a list of animals  
$cat = new Cat();  
$dog = new Dog();  
$mouse = new Mouse();  
$animals = array($cat, $dog, $mouse);  
  
// Tell the animals to make a sound  
foreach($animals as $animal) {  
	$animal->makeSound();  
}
```

Cat, Dog and Mouse are all classes that implement the Animal interface, which means that all of them are able to make a sound using the `makeSound()` method. Because of this, we can loop through all of the animals and tell them to make a sound even if we don't know what type of animal each one is.

Since the interface does not tell the classes how to implement the method, each animal can make a sound in its own way.

### Interfaces vs. Abstract Classes

Interface are similar to abstract classes. The difference between interfaces and abstract classes are:
-   Interfaces cannot have properties, while abstract classes can
-   All interface methods must be public, while abstract class methods is public or protected
-   All methods in an interface are abstract, so they cannot be implemented in code and the abstract keyword is not necessary
-   Classes can implement an interface while inheriting from another class at the same time

## Traits

### What are Traits?

PHP only supports single inheritance: a child class can inherit only from one single parent.

So, what if a class needs to inherit multiple behaviors? OOP traits solve this problem.

Traits are used to declare methods that can be used in multiple classes. Traits can have methods and abstract methods that can be used in multiple classes, and the methods can have any access modifier (public, private, or protected).

Traits are declared with the `trait` keyword:

```php
trait TraitName {  
	// some code...  
}
```

To use a trait in a class, use the `use` keyword:

```php
class MyClass {  
	use TraitName;  
}
```

Let's look at an example:

```php
trait Logger {  
	public function log($msg) {
		echo date('Y-m-d h:i:s') . ': ' $msg . "\n";
	}
}  
  
class Post{  
	use Logger; 
	
	public function create($title) {
		echo "create `$title` post\n"

		$this->log("one post was created");
	} 
	
	public function delete($title) {
		echo "delete `$title` post\n"

		$this->log("one post was deleted");
	} 
}

class User{  
	use Logger;  

	public function create($username) {
		echo "create `$username` user\n"

		$this->log("one user was created");
	} 
}  
  
$post = new Post();  
$post->create('This is the first post');

$user = new User();
$user->create('sohrab');
$user->create('reza');
```

### Using Multiple Traits

A class can use multiple traits. The following example demonstrates how to use multiple traits in the IDE class. It simulates the C compilation model in PHP for the sake of demonstration.

```php
trait Logger{
	public function log($msg) {
		echo date('Y-m-d h:i:s') . ': ' $msg . "\n";
	}
}

trait Notifyer{
	public function sms($phone, $msg) {
		echo $msg . "\n";
	}
	
	public function email($email, $msg) {
		echo $msg . "\n";
	}
}


class User{  
	use Logger, Notifyer;  

	public function create($username) {
		echo "create `$username` user\n"

		$this->log("one user was created");
		$this->sms("09120000000", "welcom to Gitmag\n Your password is 123456");
		$this->email("sohrab@gitmag.ir", "Welcome to Gitmag\n Your password is 123456");
	} 
}  

$user = new User();
$user->create('sohrab');
```

### Overriding trait method

When a class uses multiple traits that share the same method name, PHP will raise a fatal error.
Fortunately, you can instruct PHP to use the method by using the `inteadof` keyword. For example:

```php
trait FileLogger{
	public function log($msg){
		echo 'File Logger ' . date('Y-m-d h:i:s') . ':' . $msg . "\n";
	}
}

trait DatabaseLogger{
	public function log($msg){
		echo 'Database Logger ' . date('Y-m-d h:i:s') . ':' . $msg . "\n";
	}
}

class Logger{
	use FileLogger, DatabaseLogger
	{
		FileLogger::log insteadof DatabaseLogger;
	}
}

$logger = new Logger();
$logger->log('this is a test message #1');
$logger->log('this is a test message #2');
```

### Aliasing trait method 
By using aliases for the same method name of multiple traits, you can reuse all the methods in those traits.

You use the `as` keyword to alias a method of a trait to a different name within the class that uses the trait.

The following example illustrates how to alias trait method to resolve the method name conflict:

```php
trait FileLogger{
	public function log($msg){
		echo 'File Logger ' . date('Y-m-d h:i:s') . ':' . $msg . "\n";
	}
}

trait DatabaseLogger{
	public function log($msg){
		echo 'Database Logger ' . date('Y-m-d h:i:s') . ':' . $msg . "\n";
	}
}

class Logger{
	use FileLogger, DatabaseLogger
	{
		DatabaseLogger::log as logToDatabase;
		FileLogger::log insteadof DatabaseLogger;
	}
}

$logger = new Logger();
$logger->log('this is a test message #1');
$logger->logToDatabase('this is a test message #2');
```

## Static Methods & Properties

### Static Methods

Static methods can be called directly - without creating an instance of the class first.
Static methods are declared with the `static` keyword:

```php
class ClassName {  
	public static function staticMethod() {  
		// code 
	}  
}
```

To access a static method use the class name, double colon (::), and the method name:

```php
ClassName::staticMethod();
```

Let's look at an example:

```php
class greeting {  
	public static function welcome() {  
		echo "Hello World!";  
	}  
}  
  
// Call static method  
greeting::welcome();
```
Here, we declare a static method: welcome(). Then, we call the static method by using the class name, double colon (::), and the method name (without creating an instance of the class first).

### More on Static Methods
A class can have both static and non-static methods. A static method can be accessed from a method in the same class using the `self` keyword and double colon (::):

```php
class greeting {  
	public static function welcome() {  
		echo "Hello World!";  
	}  
  
	public function __construct() {  
		self::welcome();  
	}  
}  
  
new greeting();
```

Static methods can also be called from methods in other classes. To do this, the static method should be `public`:

```php
class greeting {  
	public static function welcome() {  
		echo "Hello World!";  
	}  
}  
  
class SomeOtherClass {  
	public function message() {  
		greeting::welcome();  
	}  
}
```

To call a static method from a child class, use the `parent` keyword inside the child class. Here, the static method can be `public` or `protected`.

```php
class Domain {  
	protected static function getWebsiteName() {  
		return "gitmag.ir";  
	}  
}  
  
class Gitmag extends Domain {  
	public $websiteName;  
	public function __construct() {  
		$this->websiteName = parent::getWebsiteName();  
	}  
}  
  
$gitmag = new Gitmag();  
echo $gitmag->websiteName
```

### Static Properties
Static properties can be called directly - without creating an instance of a class.
Static properties are declared with the `static` keyword:

```php
class ClassName {  
	public static $staticProp = "gitmag";  
}
```

To access a static property use the class name, double colon (::), and the property name:

```php
ClassName::staticProp;
```

Let's look at an example:

```php
class PI {  
	public static $value = 3.14159;  

	public static function get_value() {
		echo self::$value . "\n";
	}
}  
  
// Get static property  
echo PI::$value;

PI::get_value();
```
Here, we declare a static property: $value. Then, we echo the value of the static property by using the class name, double colon (::), and the property name (without creating a class first).

### late static binding

```php
class Model{
	protected static $tableName = 'Model';

	public static function getTableName(){
		return self::$tableName;
	}
}

class User extends Model{
	protected static $tableName = 'User';
}

echo User::getTableName(); // Model, not User
```

To resolve this issue, PHP 5.3 introduced a new feature called PHP static late binding.
Instead of using the `self`, you use the `static` keyword that references an exact class that is called at runtime.
Let’s modify our example above:

```php
class Model {
	protected static $tableName = 'Model';

	public static function getTableName(){
		return static::$tableName;
	}
}

class User extends Model {
	protected static $tableName = 'User';
}

echo User::getTableName(); // User
```

## Magic Methods

### __set()

So we updated all the calls to `$this->name` to return `$this->username` but what about when we want to set that value, perhaps we have an account screen where users can change their name? Help is at hand in the form of the `__set` method, and easiest to illustrate with an example.


```php
class Penguin extends Animal {

  public function __construct($id) {
    $this->getPenguinFromDb($id);
  }

  public function getPenguinFromDb($id) {
    // elegant and robust database code goes here
  }

  public function __get($field) {
    if($field == 'name') {
      return $this->username;
    }
  }

  public function __set($field, $value) {
    if($field == 'name') {
      $this->username = $value;
    }
  }
}
```

In this way we can falsify properties of objects, for any one of a number of uses. As I said, not a way to build a whole system, but a very useful trick to know.

### __get()

This next magic method is a very neat little trick to use - it makes properties which actually don't exist appear as if they do. Let's take our little penguin:

```php
class Penguin extends Animal {

  public function __construct($id) {
    $this->getPenguinFromDb($id);
  }
  public function getPenguinFromDb($id) {
    // elegant and robust database code goes here
  }
}
```
Now if our penguin has the properties "name" and "age" after it is loaded, we'd be able to do:

```php
$tux = new Penguin(3);
echo $tux->name . " is " . $tux->age . " years old\n";
```
However imagine something changed about the backend database or information provider, so instead of "name", the property was called "username". And imagine this is a complex application which refers to the "name" property in too many places for us to change. We can use the `__get` method to pretend that the "name" property still exists:

```php
class Penguin extends Animal {

  public function __construct($id) {
    $this->getPenguinFromDb($id);
  }

  public function getPenguinFromDb($id) {
    // elegant and robust database code goes here
  }

  public function __get($field) {
    if($field == 'name') {
      return $this->username;
    }
}
```
This technique isn't really a good way to write whole systems, because it makes code hard to debug, but it is a very valuable tool. It can also be used to only load properties on demand or show calculated fields as properties, and a hundred other applications that I haven't even thought of!

### __call()

There are actually two methods which are similar enough that they don't get their own title in this post! The first is the `__call` method, which gets called, if defined, when an undefined method is called on this object. The second is `__callStatic` which behaves in exactly the same way but responds to undefined static method calls instead (this was added in PHP 5.3). Probably the most common thing I use `__call` for is polite error handling, and this is especially useful in library code where other people might need to be integrating with your methods. So for example if a script had a Penguin object called $penguin and it contained `$penguin->speak()` ... the `speak()` method isn't defined so under normal circumstances we'd see:

```php
PHP Fatal error: Call to undefined method Penguin::speak() in ...
```

What we can do is add something to cope more nicely with this kind of failure than the PHP fatal error you see here, by declaring a method `__call`. For example:

```php
class Animal {
}
class Penguin extends Animal {

  public function __construct($id) {
    $this->getPenguinFromDb($id);
  }

  public function getPenguinFromDb($id) {
    // elegant and robust database code goes here
  }

  public function __get($field) {
    if($field == 'name') {
      return $this->username;
    }
  }

  public function __set($field, $value) {
    if($field == 'name') {
      $this->username = $value;
    }
  }

  public function __call($method, $args) {
      echo "unknown method " . $method;
      return false;
  }
}
```

This will catch the error and echo it. In a practical application it might be more appropriate to log a message, redirect a user, or throw an exception, depending on what you are working on - but the concept is the same. Any misdirected method calls can be handled here however you need to, you can detect the name of the method and respond differently accordingly - for example you could handle method renaming in a similar way to how we handled the property renaming above.

### __toString()

Definitely saving the best until last, the `__toString` method is a very handy addition to our toolkit. This method can be declared to override the behaviour of an object which is output as a string, for example when it is echoed. For example if you wanted to just be able to echo an object in a template, you can use this method to control what that output would look like. Let's look at our Penguin again:

```php
class Penguin {

  public function __construct($name) {
      $this->species = 'Penguin';
      $this->name = $name;
  }

  public function __toString() {
      return $this->name . " (" . $this->species . ")\n";
  }
}
```

With this in place, we can literally output the object by calling echo on it, like this:

```php
$tux = new Penguin('tux');
echo $tux;
```

I don't use this shortcut often but it's useful to know that it is there.

## Working with Objects

### Copying object via assignment
The following illustrates how to copy an object via the assignment opeator:

```php
class Person {
	public $name;

	public function __construct($name) {
		$this->name = $name;
	}
}

$sohrab = new Person('sohrab');
$ali = $sohrab;

$ali->name = 'Ali';

// show both objects
var_dump($sohrab);
var_dump($ali);
```

![enter image description here](https://raw.githubusercontent.com/gitmag-group-admin/oop_php/main/02.png)
### Copying object using the clone keyword
PHP provides you with the `clone` keyword that allows you to create a shallow copy of an object. For example:

```php
class Person {
	public $name;

	public function __construct($name) {
		$this->name = $name;
	}
}

$sohrab = new Person('sohrab');

// clone an object
$ali = clone $sohrab;
$ali->name = 'ali';

// show both objects
var_dump($sohrab);
var_dump($ali);
```

![enter image description here](https://raw.githubusercontent.com/gitmag-group-admin/oop_php/main/03.png)
### Compare Objects

in this tutorial, you will learn how to compare objects in PHP using the comparison operator ( `==`) and identity operator (`===`).

```php
class Point
{
	private $x;
	private $y;
	
	public function __construct($x, $y){
		$this->x = $x;
		$this->y = $y;
	}
}
```
When you compare objects using the comparison operator (`==`), two objects are equal if they are instances of the same class and have the same properties and values.

```php
$p1 = new Point(10, 20);
$p2 = new Point(10, 20);

if ($p1 == $p2) {
	echo 'p1 and p2 are equal.';
} else {
	echo 'p1 and p2 are not equal.';
}
```
It returns the following message:
```php
`p1 and p2 are equal`
```

When you use the identity operator (`===`) to compare objects, they are identical if and only if both of them reference the same instance of a class.

```php
$p1 = new Point(10, 20);
$p2 = $p1;

if ($p1 === $p2) {
	echo 'p1 and p2 are identical.';
} else {
	echo 'p1 and p2 are not identical.';
}
```
<table>
	<tr>
		<th>Criteria</th>
		<th>==</th>
		<th>===</th>
	</tr>
	<tr>
		<td>Two objects reference the same instance</td>
		<td>true</td>
		<td>true</td>
	</tr>
	<tr>
		<td>Objects with matching properties</td>
		<td>true</td>
		<td>false</td>
	</tr>
	<tr>
		<td>Objects with different properties</td>
		<td>false</td>
		<td>false</td>
	</tr>
</table>


## Namespaces

Namespaces are qualifiers that solve two different problems:

1.  They allow for better organization by grouping classes that work together to perform a task
2.  They allow the same name to be used for more than one class

For example, you may have a set of classes which describe an HTML table, such as Table, Row and Cell while also having another set of classes to describe furniture, such as Table, Chair and Bed. Namespaces can be used to organize the classes into two different groups while also preventing the two classes Table and Table from being mixed up.

### Declaring a Namespace

Namespaces are declared at the beginning of a file using the `namespace` keyword:

```php
namespace Html;
```

> **Note:** A `namespace` declaration must be the first thing in the PHP file. The following code would be invalid:

```php
echo "Hello World!";  
namespace Html;  
```

Constants, classes and functions declared in this file will belong to the **Html** namespace:
```php
<?php  
namespace Html;  

class Table {  
	public $title = "";  
	public $numRows = 0;  
	public function message() {  
		echo "<p>Table '{$this->title}' has {$this->numRows} rows.</p>";  
	}  
}  

$table = new Table();  
$table->title = "My table";  
$table->numRows = 5;  
?>  
  
<!DOCTYPE html>  
<html>  
<body>  
  
<?php  
$table->message();  
?>  
  
</body>  
</html>
```

For further organization, it is possible to have nested namespaces:
Declare a namespace called Html inside a namespace called Code:

```php
namespace Code\Html;
```

### Using Namespaces

Any code that follows a `namespace` declaration is operating inside the namespace, so classes that belong to the namespace can be instantiated without any qualifiers. To access classes from outside a namespace, the class needs to have the namespace attached to it.

```php
$table = new Html\Table()  
$row = new Html\Row();
```

When many classes from the same namespace are being used at the same time, it is easier to use the `namespace` keyword:

```php
namespace Html;  
$table = new Table();  
$row = new Row();
```

### Namespace Alias
It can be useful to give a namespace or class an alias to make it easier to write. This is done with the `use` keyword:

```php
use Html as H;  
$table = new H\Table();
```

```php
use Html\Table as T;  
$table = new T();
```

## Exception class

When encountering a situation from which you cannot recover, you can throw an exception.

An exception is an instance of the `Exception` class. Like other PHP objects, you use the `new` keyword to create an instance of the `Exception` class.

```php
$exception = new Exception('Invalid username or password', 100);
```

```php
$exception = new Exception('Invalid username or password', 100);

$message =  $exception->getMessage();
$code =  $exception->getCode();
```

### The throw statement
In practice, you rarely assign an exception to a variable. Instead, you raise (or throw) the `Exception` object using the `throw` statement:

```php
throw new Exception('Invalid username or password', 100);
```

```php
function divide($x, $y)
{
    if (!is_numeric($x) || !is_numeric($y)) {
        throw new InvalidArgumentException('Both arguments must be numbers or numeric strings');
    }

    if ($y == 0) {
        throw new Exception('Division by zero, y cannot be zero');
    }
    return $x / $y;
}
```

### built-in exception classes
The standard PHP library (SPL) provides many subclasses of the `Exception` class. For example, you can use the `InvalidArgumentException` when an argument of a function or method is not valid.
The following shows the exception classes in PHP 8.0:

```plaintext
Exception
   ClosedGeneratorException
   DOMException
   ErrorException
   IntlException
   JsonException
   LogicException
      BadFunctionCallException
         BadMethodCallException
      DomainException
      InvalidArgumentException
      LengthException
      OutOfRangeException
   PharException
   ReflectionException
   RuntimeException
      OutOfBoundsException
      OverflowException
      PDOException
      RangeException
      UnderflowException
      UnexpectedValueException
   SodiumException
```

###  try…catch... statement

In programming, unexpected errors are called exceptions. Exceptions can be attempting to read a file that doesn’t exist or connecting to the database server that is currently down.
Instead of halting the script, you can handle the exceptions gracefully. This is known exception handling.
To handle the exceptions, you use the `try...catch` statement. Here’s a typical syntax of the `try...catch` statement:

```php
try {
	// perform some task
} catch (Exception $ex) {
	// jump to this part
	// if an exception occurred
}

try {
	//code...
} catch (Exception1 $ex1) {
	// handle exception 1
} catch (Exception2 $ex2) {
	// handle exception 2
} catch (Exception1 $ex3) {
	// handle exception 3
}

try {
	//code...
} catch (Exception1 | Exception2 $ex12) {
	// handle exception 1 & 2
} catch (Exception3 $ex3) {
	// handle exception 3
}

try {
	// do something
} catch (Exception $e) {
	// code to handle exception
} finally {
	// code to clean up the resource
}
```

## Composer Autoload

First, create the following directory structure with files:

```php
.
├── app
│   ├── bootstrap.php
│   └── models
│       └── User.php
└── index.php
```
The `User.php` file in the `models` folder holds the `User` class:

```php
class User {
    private $username;
    private $password;

    public function __construct($username, $password) {
        $this->username = $username;
        $this->password = password_hash($password);
    }

    public function getUsername(): string {
        return $this->username;
    }
}
```

The `User` is a simple class. It has two properties `$username` and `$password`. The constructor initializes the properties from its arguments. Also, it uses the `password_hash()` function to hash the `$password`.

The `bootstrap.php` file uses the `[require_once](https://www.phptutorial.net/php-tutorial/php-require/)` construct to load the `User` class from the `User.php` file in the `models` folder:

```php
require_once 'models/User.php';
```

When you have more classes in the `models` folder, you can add more `require_once` statement to the `bootstrap.php` file to load those classes.

The `index.php` file loads the `bootstrap.php` file and uses the `User` class:

```php
require './app/bootstrap.php';
$user = new User('admin', '$ecurePa$$w0rd1');
```

This application structure works well if you have a small number of classes. However, when the application has a large number of classes, the `require_once` doesn’t scale well. In this case, you can use the `spl_autoload_register()` function to automatically loads the classes from their files.

The problem with the `spl_autoload_register()` function is that you have to implement the autoloader functions by yourself. And your autoloaders may not like autoloaders developed by other developers.

Therefore, when you work with a different codebase, you need to study the autoloaders in that particular codebase to understand how they work.

This is why Composer comes into play.

## Introduction to the Composer

Composer is a dependency manager for PHP. Composer allows you to manage dependencies in your PHP project. In this tutorial, we’ll focus on how to use the Composer for autoloading classes.

Before using Composer, you need to download and install it. The official documentation provides you with the detailed steps of how to download and install Composer on your computer.

To check whether the Composer installed successfully, you run the following command from the Command Prompt on Windows or Terminal on macOS and Linux:

```
composer -v
```

It’ll return the current version and a lot of options that you can use with the `composer` command.

### Autoloading classes with Composer

Back the the previous example, to use the Composer, you first create a new file called `composer.json` under the project’s root folder. The project directory will look like this:

```php
.
├── app
│   ├── bootstrap.php
│   └── models
│       └── User.php
├── composer.json
└── index.php
```

In the `composer.json`, you add the following code:

```php
{
    "autoload": {
        "classmap": ["app/models"]
    }
}
```

This code means that Composer will autoload all class files defined the `app/models` folder.
If you have classes from other folders that you want to load, you can specify them in `classmap` array:

 ```php
 {
    "autoload": {
        "classmap": ["app/models", "app/services"]
    }
}
```

In this example, Composer will load classes from both `models` and `services` folders under the `app` folder.

Next, launch the Command Prompt on Windows or Terminal on macOS and Linux, and navigate to the project directory.

Then, type the following command from the project directory:

```
composer dump-autoload
```

Composer will generate a directory called `vendor` that contains a number of files like this:

```php
.
├── app
│   ├── bootstrap.php
│   └── models
│       └── User.php
├── composer.json
├── index.php
└── vendor
    ├── autoload.php
    └── composer
        ├── autoload_classmap.php
        ├── autoload_namespaces.php
        ├── autoload_psr4.php
        ├── autoload_real.php
        ├── autoload_static.php
        ├── ClassLoader.php
        └── LICENSE
```

The most important file to you for now is `autoload.php` file.

After that, load the `autoload.php` file in the `bootstrap.php` file using the `require_once` construct:

```php
require_once __DIR__ . '/../vendor/autoload.php';
```

Finally, you can use the `User` class in the `index.php`:

```php
require './app/bootstrap.php';
$user = new User('admin', '$ecurePa$$w0rd1');
```

From now, whenever you have a new class in the `models` directory, you need to run the command `composer dump-autoload` again to regenerate the `autoload.php` file.

For example, the following defines a new class called `Comment` in the `Comment.php` file under the `models` folder:

```php
class Comment {
    private $comment;

    public function __construct(string $comment) {
        $this->comment = $comment;
    }

    public function getComment(): string {
        return strip_tags($this->comment);
    }
}
```

If you don’t run the `composer dump-autoload` command and use the `Comment` class in the `index.php` file, you’ll get an error:

```php
require './app/bootstrap.php';
$user = new User('admin', '$ecurePa$$w0rd1');
$comment = new Comment('<h1>Hello</h1>');
echo $comment->getComment();
```

Error:

```
Fatal error: Uncaught Error: Class 'Comment' not found in...
```

However, if you run the `composer dump-autoload` command again, the `index.php` file will work properly.

### Composer autoload with PSR-4

PSR stands for PHP Standard Recommendation. PSR is a PHP specification published by the PHP Framework Interop Group or PHP-FIG.

The goals of PSR are to enable interoperability of PHP components and to provide a common technical basis for the implementation of best practices in PHP programming.

PHP-FIG has published a lot of PSR starting from PSR-0. [For a complete list of PSR, check it out the PSR page](https://www.php-fig.org/psr/).

[PSR-4 is auto-loading standard](https://www.php-fig.org/psr/psr-4/) that describes the specification for autoloading classes from file paths. https://www.php-fig.org/psr/psr-4/

According to the PSR-4, a fully qualified class name has the following structure:

 ```
 \<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>
 ```

The structure starts with a namespace, followed by one or more sub namespaces, and the class name.

To comply with PSR-4, you need to structure the previous application like this:

```php
.
├── app
│   ├── Acme
│   │   ├── Auth
│   │   │   └── User.php
│   │   └── Blog
│   │       └── Comment.php
│   └── bootstrap.php
├── composer.json
└── index.php
```

The new structure has the following changes:

First, the `models` directory is deleted.

Second, the `User.php` is under the `Acme/Auth` folder. And the `User` class is namespaced with `Acme/Auth`. Notice how namespaces map to the directory structure. This also helps you find a class file more quickly by looking at its namespace.

```php
namespace Acme\Auth;

class User {
    // implementation
    // ...
}
```

Third, the `Comment.php` is under the `Acme/Blog` folder. The `Comment` class has the namespace `Acme\Blog`:

```php
namespace Acme\Blog;

class Comment {
    // implementation
    // ...
}
```

Fourth, the `composer.json` file looks like the following:

```php
{
    "autoload": {
        "psr-4": {
            "Acme\\":"app/Acme"
        }
    }
}
```

Instead using the `classmap`, the `composer.json` file now uses `psr-4`. The `psr-4` maps the namespace `"Acme\\"` to the `"app/Acme"` folder.

Note that the second backslash (`\`) in the `Acme\` namespace is used to escape the first backslash (`\`).

Fifth, to use the `User` and `Comment` classes in the `index.php` file, you need to run the `composer dump-autoload` command to generate the autoload.php file:

```
composer dump-autoload
```


Since the `User` and `Comment` classes have namespaces, you need to have the `use` statements in `index.php` as follows:

```php
require './app/bootstrap.php';

use Acme\Auth\User as User;
use Acme\Blog\Comment as Comment;

$user = new User('admin', '$ecurePa$$w0rd1');

$comment = new Comment('<h1>Hello</h1>');
echo $comment->getComment();
```
