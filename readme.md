Lesson 1. Design patterns. Singletone
=====================================

* ***Actions on the deployment of the project:***

- Making a new project dpcreate-singletone_webformyself.loc:
																	
	sudo chmod -R 777 /var/www/DESIGN_PATTERNS/Creational/dpcreate-singletone_webformyself.loc

	//!!!! .conf
	sudo cp /etc/apache2/sites-available/test.loc.conf /etc/apache2/sites-available/dpcreate-singletone_webformyself.loc.conf
		
	sudo nano /etc/apache2/sites-available/dpcreate-singletone_webformyself.loc.conf

	sudo a2ensite dpcreate-singletone_webformyself.loc.conf

	sudo systemctl restart apache2

	sudo nano /etc/hosts

	cd /var/www/DESIGN_PATTERNS/Creational/dpcreate-singletone_webformyself.loc

- Deploy project:

	`git clone << >>`
	
	`or Download`
	
	_+ Сut the contents of the folder up one level and delete the empty one._
																							
---

WebForMySelf

[Lesson 1. Design patterns. Singleton (37:05)]( https://www.youtube.com/watch?v=NNk05iKtmPs&ab_channel=WebForMySelf )

Continuation of the course on design patterns here: 
<https://webformyself.com/category/premium/php-premium/patterns-premium/>

Welcome to the first lesson of the Premium Course on Learning Design Patterns in PHP.
For the sake of fairness, it should be noted that patterns - this concept is relevant for any language that supports an object-oriented approach to programming.
This means that patterns describe some kind of interaction between classes.

Directly in this video, we will define the concept of design patterns, that is, we will talk about what it is, why they are used, what problems they solve, what groups they are divided into, and whether it is worth studying this topic at all.

In addition, we will look at one of the representatives of the group of generative patterns - the Singletone design pattern.
Thus, you will learn in what cases it is convenient to use it, what basic conditions must be observed for its implementation and, of course, how to implement it.

[(0:45)]( https://youtu.be/NNk05iKtmPs?t=45 ) Design Pattern or Design Pattern is a common solution to a specific problem when designing the architecture of a web application or any other program.
In fact, this is a way to solve recurring problems, that is, some typical tasks. BUT you must understand that a Pattern is NOT a Library and NOT a specific set of functions OR methods.
That is, this is NOT a ready-made solution that can be taken and copied into your project. - This is, first of all, a method OR a certain technique for solving a particular problem that will need to be written independently and,
 possibly, adapted for a specific implementation.

[(1:40)]( https://youtu.be/NNk05iKtmPs?t=100 ) Just as Patterns should NOT be confused with Algorithms because IF an Algorithm provides a clear set of actions, then a Pattern is ONLY just a description of a solution to a problem, the implementation of which, of course, may be different.

[(2:00)]( https://youtu.be/NNk05iKtmPs?t=120 ) As a rule, IF we are talking about Patterns, then the following main points are highlighted:

1. The problem that the Pattern solves.
2. The class structure constituting an immediate solution.
3. Approximate implementation.

[(3:25)]( https://youtu.be/NNk05iKtmPs?t=205 ) Patterns provide proven solutions that can save you a lot of time. They also provide code standardization, which helps to reduce errors and miscalculations in the implementation.
Patterns provide a general approach to solving a problem, which makes it possible to systematize and technically correctly describe the structure of your project. Using Patterns it is much easier to explain how a certain part of the system works.

[(4:30)]( https://youtu.be/NNk05iKtmPs?t=270 ) There are many Patterns of varying levels and complexity, level of detail and coverage of system design. They are grouped and classified according to these characteristics.

Idioms - Patterns of the lowest level. They are NOT universal as they are ONLY applicable within one specific programming language.

The most universal Patterns - which can be implemented in absolutely any programming language.
By design, there are 3 main groups:
1. Generators - are used for a specific image Creation of new objects WITHOUT introducing unnecessary dependencies into the program.
2. Structural Patterns - show different ways of building connections between objects. That is, the Patterns that are responsible for the formation of the Structure of your project.
3. Behavioral Patterns - used to implement effective communication between objects. In fact, this is also a kind of Connection, but this is more related to communication, the exchange of data between objects.

[(7:30)]( https://youtu.be/NNk05iKtmPs?t=450 ) `Creational Patterns. Singletone`.
There have been quite a lot of discussions about Singletone lately. Some programmers call it Antipattern and, accordingly, urge NOT to use it in their projects. BUT Singletone is a Pattern to start with.
He is very good at identifying a problem and showing how to solve it. Singletone - A Generative Pattern whose design ensures that a class has ONLY one instance and provides some kind of global access point to this class.
Very often, in an application you are developing, you need to provide ONLY one single object or instance of a given class. It can be a database connection object, an object that writes something to a file, perhaps logs.

[(9:50)]( https://youtu.be/NNk05iKtmPs?t=590 ) Of course, this Pattern has certain drawbacks, which are somewhat reminiscent of the drawbacks of global variables.
IF we use it in a certain system, then in the presence of various modules that imply the only Creation of an object, then this Pattern must be placed in each module. It is also somewhat inconvenient.

[(10:30)]( https://youtu.be/NNk05iKtmPs?t=630 ) `Coding.`

```
classes 			 - folder with Pattern classes
	Singletone		 - the folder contains a class that implements the Singletone Pattern.
		FileSave.php - is a class that implements the Singletone Pattern.
functions.php		 - file with class connection function
index.php 			 - entry point
```

[(26:35)]( https://youtu.be/NNk05iKtmPs?t=1595 ) `In Browser`.

	http://dpcreate-singletone_webformyself.loc/

[(26:40)]( https://youtu.be/NNk05iKtmPs?t=1600 ) `TXT-file`. 

_The content of the file is "text" + Let's delete it(file)._

[(27:05)]( https://youtu.be/NNk05iKtmPs?t=1625 ) Create 4 objects in `index.php` + Refresh Browser(F5).

```php 
use Singletone\FileSave;

require "functions.php";
spl_autoload_register('project_autoload');

$file = new FileSave();
$file->save(__DIR__);

$file = new FileSave();
$file->save(__DIR__);

$file = new FileSave();
$file->save(__DIR__);

$file = new FileSave();
$file->save(__DIR__);
```

_See 4 files_

The problem is obvious. That is, in our current project it is necessary to guarantee a single instance of a specific class.
BUT we see that we have the right to Create multiple instances, and thus our script must add some content to the same file, and instead it Creates 4 files.
Which is unacceptable.

[(27:45)]( https://youtu.be/NNk05iKtmPs?t=1665 ) `Singleton solves the problem.`

Let's modify the FileSave class to follow the Singletone Design Pattern.

[(28:10)]( https://youtu.be/NNk05iKtmPs?t=1690 ) In `FileSave.php`:

The first thing to do is to declare the constructor of this class private. This will make it impossible to create an object of this class directly.

```php
...
private function __construct(){
...
```

[(28:14)]( https://youtu.be/NNk05iKtmPs?t=1694 ) 

Error:

_We are trying to access a private constructor method. - And the constructor is executed when creating an object of the class._

[(28:30)]( https://youtu.be/NNk05iKtmPs?t=1710 ) 

IF we are talking about the "uniqueness" of an instance of the class being created, then of course, this instance must be stored somewhere. - Let's create a private static property. And this property will store an object of the specified class.
Why static, because a static property refers to a class, NOT a specific object.

```php
private static $_instance;
```

[(29:00)]( https://youtu.be/NNk05iKtmPs?t=1740 ) 

_We need an intermediary method that will create OR return an object of this class, `public static getInstance()`._

[(33:05)]( https://youtu.be/NNk05iKtmPs?t=1985 ) `__clone()` & `__wakeup()`. 

_In order to really NOT be able to Create an object of this class, it is necessary to declare these methods as private._

[(34:05)]( https://youtu.be/NNk05iKtmPs?t=2045 ) `index.php`:

```php
use Singletone\FileSave;

require "functions.php";
spl_autoload_register('project_autoload');

$file = FileSave::getInstance();
$file->save(__DIR__);

$file = FileSave::getInstance();
$file->save(__DIR__);

$file = FileSave::getInstance();
$file->save(__DIR__);

$file = FileSave::getInstance();
$file->save(__DIR__);
```

[(34:30)]( https://youtu.be/NNk05iKtmPs?t=2070 ) `Refresh Browser(F5).`

![screenshot of sample]( https://github.com/mslobodyanyuk/dpcreate-singletone_webformyself/blob/main/public/images/firefox.png )

_Go to the root of our project and see one single file._

![screenshot of sample]( https://github.com/mslobodyanyuk/dpcreate-singletone_webformyself/blob/main/public/images/xubuntu.png )

Content that intended to receive:

![screenshot of sample]( https://github.com/mslobodyanyuk/dpcreate-singletone_webformyself/blob/main/public/images/kate.png )

```
 text text text text
``` 

_- Four times written string. That is, we have added the specified file._

[(34:50)]( https://youtu.be/NNk05iKtmPs?t=2090 ) Thus, no matter how many objects of the class we created, IF the Singletone design pattern is used,
then we thus necessarily guarantee the uniqueness of the uniqueness of the created object of the class.

[(35:30)]( https://youtu.be/NNk05iKtmPs?t=2130 )The Singletone design pattern is somewhat less used now than it used to be because some define it as the Antipattern.
BUT you definitely need to know it because it is quite common in various projects. And, of course, he very well demonstrates the solution to a specific problem.

Again, the implementation can be different:
- The condition in `getInstance()` can be written in different ways.
- You can store an object of a specific class in different ways.
- You can return an object in some unique way.

The implementation may be different, BUT the meaning, the very essence remains the same:

1. First, it is imperative that we Close the constructor and ALL possible magic methods that allow us to Create an object of the specified class, that is, we Close the direct Creation of an object.
2. And then we form a method that will return a single instance of this class.

#### Useful links:

WebForMySelf

[Lesson 1. Design patterns. Singletonе]( https://www.youtube.com/watch?v=NNk05iKtmPs&ab_channel=WebForMySelf )

<https://webformyself.com/category/premium/php-premium/patterns-premium/>