[![forthebadge](http://forthebadge.com/images/badges/uses-js.svg)](http://forthebadge.com)


# JavaScript


## Table of Contents

1. [Definitions](#definitions)
1. [Basic Concepts](#concepts)
1. [Scope](#scope)
1. [Arrays](#arrays)
1. [Functions](#functions)
1. [Closers](#closers)
1. [Callbacks](#callbacks)
1. [Objects](#objects)
1. [Loops](#loops)
1. [Conditional Statements](#statements)
1. [JSON](#json)
1. [Misc](#misc)
1. [Credits](#credits)


## Definitions


- **Syntax Parser:** A program that reads your code and what it does and if it's grammar is valid.
- **Lexical Environment:** Where something sits in the code you write. Where is it written and what surrounds it, is important.
- **Execution Context:** A wrapper to help manage the code that is running.
- **Dynamic Typing:** JavaScript is a _loosely typed_ or a _dynamic_ language. That means you don't have to declare the type of a variable ahead of time. The type will get determined automatically while the program is being processed.


## Basic Concepts

- **Name/Value Pairs:** A name which maps to a unique value.

	Example:

	```javascript
	
	{
		Person: 'John Doe'
	}

	// In this example, 'Person' is the name and 'John Doe' is the value.

	```

	```javascript

	Person : {
    Name : 'John Doe',
    Age: 45,
    Address: {
          Street: '4321 Watt Way',
          City: 'San Diego',
          State: 'CA',
          Zip: 89765
     }
	}

	// In this example, 'Person' becomes a collect of other name/value pairs

 	```

	 - The name may be defined more than once, but only can have one value in any given context.
	 - Furthermore, that value may have more name/value pairs (as shown in the second example).
	 - When talking about Objects in JavaScript, we are talking about a collection of name/value pairs 

See [Objects](#objects) for a more in depth look. 

- **The Global Environment and the Global Object:**
	-- Whenever code is run in JavaScript, it's run inside an Execution Context (i.e., an execution wrapper).
	-- By default, JavaScript automatically create two things for you:
		1. The Global Object
		2. The 'this' variable


- **Dynamic typing:**

  Supporting article: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

  Example:

	```javascript

  // Note: You can have the same variable as different types.

  var foo = 42;        // foo is now a Number
  var foo = "bar";     // foo is now a String
  var foo = true;      // foo is now a Boolean

  ```

- **Data types:** ECMAScript standards define seven data types:

  - Six data types that are primitives
    - Boolean
    - Null
    - Undefined
    - Number
    - String
    - Symbol (new in ECMAScript 6)

  - Object


## Scope


- **Global & Local Variable:**

	```javascript

	var name = "joe"; // global

	function DoStuff() {

		var name = "john"; // local to doStuff

	}

	```



## Arrays 

- **How to create an Array using String Values:**

	```javascript

	var names = ["jim", "john", "joe"];

	```

- **How to adding a new value to an Array:**

	```javascript

	var names = ["jim", "john", "joe"];

	names.push("sam");

	// see what is returned you the browser console
	console.log(names); = names = ["jim", "john", "joe", "sam"];

	```


- **Creating an Array using numbers:**

	```javascript

	var values = [10, 20, 30, 40, 50];

	// How to Reverse the values in an Array
	var reversedValues = values.reverse();

	// Output: 50,40,30,20,10

	```


## Functions


#### Types: Declarative vs Expressive:

- Additional Articles by: 

	-	[Angus Croll](http://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)
	- [John Papa](http://www.johnpapa.net/angular-function-declarations-function-expressions-and-readable-code/)

- **Declarative:**

	```javascript

	// function statement
	function Foo() {
	    return 3;
	}

	Foo(); // return 3 

	```

- **Expressive:**

	```javascript

	// anonymous function expression
	var a = function() {
	    return 3;
	}

	// OR

	(function() {
	    alert('Hello');
	}) ();


	// named function expression
	var a = function bar() {
	    return 3;
	}

	// self envoking function expression
	(function sayHello() {
	    alert('Hello');
	}) ();

	```

#### Functions In Action


- **Basic Function:**

	```javascript

	function SayHello() {
	    alert('Hello');
	}

	SayHello(); // Calls the function

	```

- **Creating a Function that takes Arguments:**

	```javascript

	function ShowDistance(speed, time) {
	    alert(speed + time);
	}

	ShowDistance(10, 5); // Calls the Function and the Values we pass to it – returning the value 15

	```

- **Creating a Function that Returns Data:**

	```javascript

	function ShowDistance(speed, time) {
	    alert(speed + time);
	}

	var myDistance = ShowDistance(10, 5); // Store the results of the calculation showDistance does

	myDistance(); // Calls the results of showDistance = 15

	```


- **Create a Function Literal:**

	- _Note: A function literal is a function without an assigned name._

	```javascript

	var add = function(a, b) {
	    return a + b;
	}

	add(10, 5); // Calls the Function and the Values we pass to it – returning the value 15

	```

- **Create Constructor Function:**

	```javascript

	function Cars(make, model, year) {

	    this.make = make;
	    this.model = model;
	    this.year = year;
	}

	var car1 = new Cars("Toyota", "Tacoma", "2014"); // new instances of the object Cars
	var car2 = new Cars();

	```

- **How to add a custom method to the Cars object:**

	```javascript

	Cars.prototype.price = function() {

	    alert("$25,000.00");

	} // All instances of the object Cars will inherit this method

	console.log(car1);
	// ^output: Cars {make: Toyota, model: Tacoma, year: 2014, price: function}

	```


- **Another use of a Constructor Function and Prototype:**

	```javascript

	function Person(name) {
	    this.name = name;
	}
	// When called as a constructor, the above will create a named property 
	// of an instance called name and assign it the value of the name parameter.

	Person.prototype.greet = function(otherName) {
	    return "Hi" + otherName + ", my name is" + this.name;
	}
	// Here the identifier name is used as a variable, but the identifier you are 
	// looking for is a named property of the instance, so you need to access it 
	// as such. Typically, this function will be called as a method of the instance 
	// so this within the function will be a reference to the instance.


	var john = new Person("John");
	// Here we create a new instance of Person
	// Assign it to a new object called 'jonh'
	// And passed in a new string property (i.e., "John")
	//
	// Note: Variables starting with a capital letter are, by convention, reserved for construtors)

	// and then
	john.greet("Fred"); // Returns: Hi Fred, my name is John.

	```



## Closers

A closure is a set of local variables inside a function – kept alive after the function has returned.

- **Basic Closer:**

	```javascript

	function ShowName() {

		var name = "joe";

	  	return name; // makes var name accessable in the global space 

	}

	var showNames = ShowName(); // this creates a variable in the global space which keeps the local variable (name) alive for further use.


	// console.log(showName); will return the word "Hello"

	```

- **Basic Closer - Using Arguments:**

	```javascript

	function GetDistance(speed, time) { // passes the arguments

	    var distance = speed * time; // stores the arguments values

	    return distance; // make the values accessable in the global space

	}

	var myDistance = getDistance(10, 5);
	// When the getDistance function gets called, 
	// it gets evaluated and returns a numerical value that 
	// then becomes assigned to the myDistance variable.

	console.log(myDistance);


	// Quick Aside:
	// 'this' represent the scope of context for the closer you're actually in

	function Avengers() {

		this.avengers = [];

	}

	// OR

	function Avengers() {

	    var vm = this;

	    vm.avengers = [];

	}

	```

## Callbacks


- **Simple jQuery example:**

	```javascript

	$("button").click(function(){
	  $("p").hide("slow",function(){
	    alert("The paragraph is now hidden"); // waits until the hide function has successfully ran
	  });
	});

	```

- **How to pass an Anonymous function to a Method as a parameter**

	```javascript

	var names = ['Mike', 'John', 'Bill']; //stores an array of names in a variable

	names.forEach(
	    function(eachName, index) {
	        alert(index + 1 + '.' + eachName);
	    }
	);  //1st: assigns the names varaible to the forEach method
	    //2nd: we pass our anonymous function to the forEach method as a parameter
	    //3rd: we pass in two parameters to our anonymous function (eachName = the array of name strings, index = our counter which is iterating through our array of names and incrementing our integer (1) value) 
	    //lastly, our results are output in an alert modole.

	```

- **Create a class call setSelected:**

	```javascript

	function SetSelected() {

		// When a tab is clicked we need to remove the class 'selected', from the previously active tab and assign it to the new tab being clicked

		var tab = document.querySelector('.tab');

		tab.addEventListener('click', function() { // this is an anonymous function

			var active = document.querySelectorAll('.tab.is-selected');

	  	ValidateSelected(this, active);

	  	//In the above we are passing 2 arguments through the function 'validateSelected'

	  	//this = the element being clicked (tab) - this is being passed in the below function as (elem)
	  	//active = the active element (i.e. The one with class 'is-selected' applied to it)

	  )};
	}

	function ValidateSelected(elem, active) {

	  // elem = tab being clicked
	  // active = tab last selected

	  var this = elem, //here we assign elem to a variable named this
	      that = this.closest('.tab-wrapper').find(active);
	      
	  //that grabs the active element, then bubbles up the DOM tree and 
	  //grabs the closest parent element with the assigned class name (tab-wrapper)

	  that.removeClass('selected'); //when tab is clicked, we remove the class 'selected' from the previously clicked tab
	  this.addClass('selected'); //and assign the newly clicked tab with the class 'selected' 

	}

	SetSelected(); //call the function

	// [Note]: 
	// validateSelected doesn't execute until initSelected is triggered and finished
	// A callback function is executed after the current effect is finished.

	```


## Objects

- **Aside:**

	- All data (variables), with properties and methods. 
	- Almost everything in javascript can be an object... Functions, Variable, Strings, Arrays

- **By Value vs By Reference:**
	- _Note: It's important to understand the differences between the two._
	```javascript
	
	// by value

	var a = 3;            // 3 is a primitive value (Number)
	var b;

	b = a;                // assigns a copy of (a's) value

	console.log(b);       // will be 3

	// Why? Both (a & b) point to new spots (addresses) in memory.
	//      Since (a) is a primitive value - (b) can recieve a copy of it's value    


	**************************************************************************************

	// by reference (all objects (including functions))

	var a = { greeting: 'hi' };    // object literal
	var b;

	b = a;                         // points (b) to the same stop in memory as (a) 

	// Why? Both are objects. (b) simply become a reference of (a). It doesn't get set up as
	//      a new place in memory, as a copy of (a)

	// This means, (b) can mutate (a's) property value

	b.greeting = 'hello';

	console.log(a);                // will be 'hello'
	console.log(b);                // will be 'hello'

	// Why? Both are pointing to the same location in memory, which was updated (mutated) by (b)

	```


- **Create an Object:**

	```javascript

	var Person = {};

	// Assign a method to that object

	Person.SayHello = function() {

	  alert("Hello");

	}

	```

- **Create a global namespaced object and assign it a method:**

	```javascript

	var Person = {

	  SetMessage: function() {

	    alert("Hello");

	  }

	};

	// to call SayHello and run the alert

	var getMessage = Person.SetMessage();

	getMessage();

	```

- **You can also create a re-usable object know as a 'First Class Function' in JavaScript:**
	- _First Class Functions: Everything you can do with other types you can do with functions. You can assign them to variables, pass them around, create them on the fly._


	```javascript

	function Message() {

	  this.hello = function() {

	  	alert("Hello World");

	  }

	}

	var message1 = new Message(); //message1 becomes a new instance of the object Message

	message1.hello();

	```

- **How to assign a new property to an Object:**

	```javascript

	// Object literal
	var Person = {

	  //property
	  firstName: "john";

	};

	// Or

	var Person = {};

	Person.firstName = "joe";

	var nameVal = Person.firstName;

	alert(nameVal);

	```

- **You can also assign a method to a property of an Object:**

```javascript

var Person = {

  //properties
  firstName: "John", 
  lastName: "Doe", 
  age: 30,

	// the method
  personsInfo: function(){
    eturn this.firstName + " " + this.lastName + " is " + this.age + ".";
  }
};

var setPersonsInfo = Person.personsInfo();

console.log(setPersonsInfo); // should return: John Doe is 30

```


#### Object Literals

 - An object literal is a comma-separated list of name-value pairs wrapped in curly braces. 
 - Object literals encapsulate data, enclosing it in a tidy package. This minimizes the use of global variables which can cause problems when combining code.

```javascript

var MyObject = {
  string: 'string value',
  number: 40,
  bool: true 
}

```


## Loops

- **While loop:**

	```javascript

	// set up the index
	var i = 1;

	// create the counter or check the condition
	while (i < 10) {
		i++; // increment the index
	}

	```

- **For loop:**

	```javascript

	// set index, check condition, increment index
	for (var i = 1; i < 10; i++) {
	  // do stuff
	}

	```

- **Quick Aside:**
	- All three expressions in the head of the for loop are optional.

	```javascript

	// For example, in the initialization block it is not required to initialize variables

	var i = 0;

	for (; i < 9; i++) {
		console.log(i);
	}

	// Remember to include a semi-colon in-place of any omited expressions (shown above)

	```

- **For loop using a break:**

	```javascript

	for (var i = 1; i < 10; i++) {

	    // do stuff

	    if (i == 101) {
	    	break;
	    	// break jumps out of the loop once the condition is met
	    }
	}

	```

- **For loop using a continue:**

	```javascript

	for (var i = 1; i < 10; i++) {
	  // do stuff
	  if (i % 5 == 0) {
	  	continue; // done with this iteration, not the entire loop, just this time around
	  }
	  // do second set of stuff
	}

	```

## Conditional Statements


- **How to create a basic condition:**

	```javascript

	var a = 1,
	  b = 100;

	if(a < b) {
	  alert("a is less than b");
	}

	```


- **How to create multiple conditions:**

	```javascript

	var time = new Date().getHours();

	var morning = 10,
    afternoon = 20;

    if(time < morning) {
	    // if condition 1 is true
	    alert("Good Morning");
    } 
    else if (time < afternoon) {
      // if condition 2 is true
      alert("Good Afternoon");
    } 
    else {
      // if both condition are false
      alert("Good Night");
    }

	```

- **How to write a 'Ternary' condition:**

	```javascript

	var now = new Date();
	var greeting = "Good" + ((now.getHours() > 17) ? " evening." : " day.");

	// greeting = the test
	// evening = expression1 - wich is returned is the test is true
	// day = expression2 - wich is returned is the test is false

	console.log(greeting);

	```


## JSON

- **Create JSON Object Key - Value Pairs:**

	```javascript

	var people = {

	    person: [

	        {
	            "user": "eric",
	            "age": 30
	        }, {
	            "user": "levi",
	            "age": 31
	        }

	    ]

	}

	```

- **How to parse the JSON object:**

	```javascript

	function CreateList() {

	    var data = people.person;

	    data.forEach(function (key, item) {

	        var user = item.user,
	            age = item.age,
	            html = [];

	        html.push('<p> + user + </p>');
	        html.push('<p> + age + </p>');


	        var build = html.join();

	    });
	}

	CreatList(); // call function

	console.log(CreateList);

	```

## Misc

- **How to create a string:**

	```javascript

	var str = "a b c";

	```

- **How to reverse the above string:**

	- There are a few different ways to accomplish this here are three.
	
	```javascript
	// chaining methods
	
	function reverseString (str) {
	
		return str.split('').reverse('').join('');	
	}
	
	console.log(reserveString( 'Hello' ));      // should result in 'olleH'
	
	
	```
	
	```javascript
	// create a decrementing For Loop

	function reverseString (str) {
	
		// stand up our empty string
		var reverse = '';
		
		for (var i = str.length -1; i >= 0; i--) {
		
			reverse += str[i]; // assign results to reverse
		
		}
		
		return reverse;
	
	} 
	
	console.log(reverseString('Hello'));      // should result in 'olleH'

	```
	
	- Now that we have a reusable function at our disposol, we could re-reverse our 'olleH' string
	
	```javascript
	
	// using the function above, we can do the following
	
	// store our result in a new variable
	var reversedString = reverseString('Hello');
	
	// then pass that variable back into our reverseString function
	var str = reverseString(reversedString);
	
	console.log(str);                        // should result in 'Hello'
	
	```

	```javascript

	// using a recursive strategy

	function reverse (str) {

	    if (str === "") {

	        return "";

	    } else {

	        return reverse(str.substr(1)) + str.charAt(0);

	    }

	}

	console.log(reverse( 'Hello' ));

	```

- **How to reverse alpha only characters in a given string:**

	```javascript

	/**
	 * Objective: Reverse each word in the given string, 
	 * leaving both the sequence and any special characters untouched. 
	 */

	// Our reverse function
	function ReverseString (str) {

	  // Step 1. Create an empty string that will host the new created string
		var newString = '';

	  // Step 2. Create our FOR loop
	  /* The starting point of the loop will be (str.length - 1) which corresponds to the
	   * last character of the string.
	   * As long as i is greater that or equal to 0, the loop will go on.
	   * We decrement i after each iteration
	   */
		for (var i = str.length - 1; i >= 0; i-- ) {

			newString += str[i]; // newString = newString + str[i]

		}

	  // Step 3. Return the reversed string
		return newString;

	}

	// Create a new function that will match and replace only characters a-z (alpha only)
	function ReverseAlphaOnly (str) {

	  // Returns a new string with only those matching the provided Regexp (Regular Expression Pattern)
		return str.replace(/[a-z]+/gi, function(matches) {

	    // Next, we reverse our matched words
			var stringOut = ReverseString(matches);

	    // Return our new string
			return stringOut;

		});

	}

	// Now we can define the string we want to reverse.
	var revStr = ReverseAlphaOnly('Hi! my, !name is > Eric');

	console.log(revStr);    // should result in 'iH! ym, !eman si > cirE'


	```


- **How to turn a string into an array:**

	```javascript
	
	function createNewArray (str) {
	
		var newArray = [];
		var items = str.split('');
		
		for ( var i = 0; i < items.length; i++ ) {
		
			newArray.push(items[i]);
		
		}
		
		return newArray;
	
	}
	
	var newArray = createNewArray('Hello');
	
	console.log(newArray);
	
	```

- **How to create a simple filter:**

	```javascript
	
	var messages = [{ "message": "one" }, { "message": "two" }, { "message": "three" }];
	var message = 'two';
	var foundMessage = false;

	for (var i = 0; i < messages.length; i++) {

  		if (messages[i].message == message) {

    		foundMessage = true;
    		break;

  		}
	}
	
	```




## Credits:

- [Anthony Alicea](https://www.udemy.com/user/anthonypalicea/)
- [Todd Motto](https://toddmotto.com/)

**[Back to top](#table-of-contents)**
