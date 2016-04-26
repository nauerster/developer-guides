[![forthebadge](http://forthebadge.com/images/badges/uses-js.svg)](http://forthebadge.com)


# JavaScript


## Table of Contents

1. [Scope](#scope)
2. [Arrays](#arrays)
3. [Functions](#functions)
4. [Closers](#closers)
5. [Callbacks](#callbacks)
6. [Objects](#objects)
7. [Loops](#loops)
8. [Conditional Statements](#statements)
9. [JSON](#json)



## Scope


- **Global & Local Variable:**

	```javascript

	var name = "joe"; // global

	function doStuff() {

		var name = "john"; // local to doStuff

	}
	
```



## Arrays 


```javascript
// Create an Array using String Values:

var names = ["jim", "john", "joe"];
```

```
// Adding a new value to the Array:

var names = ["jim", "john", "joe"];

names.push("sam");

//console.log(names); = names = ["jim", "john", "joe", "sam"];


// Create an Array using numbers:

var values = [10, 20, 30, 40, 50];

// How to Reverse the values in an Array
var reversedValues = values.reverse();

// Output: 50,40,30,20,10



/* --------------------------------------------- */
// [3] Functions
/* --------------------------------------------- */

// Types: Declarative vs Expressive
// url: http://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/

// Declarative:

function foo() {
    return 3;
}

foo(); // return 3 


// Expressive:

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



// Functions In Action
/* --------------------------------------------- */

// Basic Function

function sayHello() {
    alert('Hello');
}

sayHello(); // Calls the function



// Creating a Function that takes Arguments

function showDistance(speed, time) {
    alert(speed + time);
}

showDistance(10, 5); // Calls the Function and the Values we pass to it – returning the value 15



// Creating a Function that Returns Data

function showDistance(speed, time) {
    alert(speed + time);
}

var myDistance = showDistance(10, 5); // Store the results of the calculation showDistance does

myDistance(); // Calls the results of showDistance = 15



// Create a Function Literal - Note: A function literal is a function without an assigned name
var add = function(a, b) {
    return a + b;
}

add(10, 5); // Calls the Function and the Values we pass to it – returning the value 15


// Create Constructor Function

function Cars(make, model, year) {

    this.make = make;
    this.model = model;
    this.year = year;
}

var car1 = new Cars("Toyota", "Tacoma", "2014"); // new instances of the object Cars
var car2 = new Cars();


// How to add a custom method to the Cars object

Cars.prototype.price = function() {

    alert("$25,000.00");

} // All instances of the object Cars will inherit this method

console.log(car1);
// ^output: Cars {make: Toyota, model: Tacoma, year: 2014, price: function}



// Another use of a Constructor Function and Prototype 


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





// [4] Closers
/* --------------------------------------------- */
// A closure is a set of local variables inside a function – kept alive after the function has returned.

// Basic closer

function showName() {

    var name = "joe";

    return name; // makes var name accessable in the global space 

}

var showNames = showName(); // this creates a variable in the global space which keeps the local variable (name) alive for further use.


// console.log(showName); will return the word "Hello"


// Basic Closer - Using Arguments

function getDistance(speed, time) { // passes the arguments

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


// [5] Callbacks
/* --------------------------------------------- */


// Simple jQuery example

$("button").click(function(){
  $("p").hide("slow",function(){
    alert("The paragraph is now hidden"); // waits until the hide function has successfully ran
  });
});


// How to pass an Anonymous function to a Method as a parameter

var names = ['Mike', 'John', 'Bill']; //stores an array of names in a variable

names.forEach(
    function(eachName, index) {
        alert(index + 1 + '.' + eachName);
    }
);  //1st: assigns the names varaible to the forEach method
    //2nd: we pass our anonymous function to the forEach method as a parameter
    //3rd: we pass in two parameters to our anonymous function (eachName = the array of name strings, index = our counter which is iterating through our array of names and incrementing our integer (1) value) 
    //lastly, our results are output in an alert modole.


// create a class call setSelected

function setSelected() {

    //When a tab is clicked we need to remove the class 'selected', from the previously active tab and assign it to the new tab being clicked

    $('.tab').on('click', function() {// this is an anonymous function

            var active = $('.tab.selected');

            validateSelected(this, active);

            //In the above we are passing 2 arguments through the function 'validateSelected'

            //this = the element being clicked (tab) - this is being passed in the below function as (elem)
            //active = the active element (i.e. The one with class 'selected' applied to it)
    });
}

function validateSelected(elem, active) {

    //elem = tab being clicked
    //active = tab last selected

    var this = $(elem), //here we assign elem to a variable named this
        that = this.closest('.tab-wrapper').find(active);
    //that grabs the active element, then bubbles up the DOM tree and 
    //grabs the closest parent element with the assigned class name (tab-wrapper)

    that.removeClass('selected'); //when tab is clicked, we remove the class 'selected' from the previously clicked tab
    this.addClass('selected'); //and assign the newly clicked tab with the class 'selected' 

}

setSelected(); //call the function

// [Note]: 
// validateSelected doesn't execute until initSelected is triggered and finished
// A callback function is executed after the current effect is finished.




// [6] Objects
/* --------------------------------------------- */

// [Note]:
// All data (variables), with properties and methods. 
// Almost everything in javascript can be an object... Functions, Variable, Strings, Arrays


// Create an Object:

var Person = {};



// Assign a method to that object

Person.SayHello = function() {

    alert("Hello");

}


// Create a global namespaced object and assign it a method

var Person = {

    SetMessage: function() {

        alert("Hello");

    }

};

// to call SayHello and run the alert

var getMessage = Person.SetMessage();

getMessage();



// You can also create a re-usable object know as a 'class function' in javascript:

function Message() {

    this.hello = function() {

        alert("Hello World");

    }

}

var message1 = new Message(); //message1 becomes a new instance of the object Message

message1.hello();


// Assingn a new property to an Object:

var Person = {

    //property
    firstName: "john";

};


// Or

var Person = {};

Person.firstName = "joe";

var nameVal = Person.firstName;

alert(nameVal);


// You can also assign a method to a property of the object

var Person = {

    //properties
    firstName: "John", lastName: "Doe", age: 30,

    personsInfo: function(){
        return this.firstName + " " + this.lastName + " is " + this.age + ".";
    }
};

var setPersonsInfo = Person.personsInfo();

console.log(setPersonsInfo); // should return: John Doe is 30



// Object Literals
/* --------------------------------------------- */
// An object literal is a comma-separated list of name-value pairs wrapped in curly 
// braces. Object literals encapsulate data, enclosing it in a tidy package. This minimizes 
// the use of global variables which can cause problems when combining code.

var MyObject = {
    string:  'string value',
    number:  40,
    bool:    true 
}




// [7] Loops
/* --------------------------------------------- */


// While loop

// set up the index
var i = 1;
// create the counter or check the condition
while (i < 10) {
    i++; // increment the index
}


// For loop

// set index, check condition, increment index
for (var i = 1; i < 10; i++) {
    // do stuff
}


// For loop using a break

for (var i = 1; i < 10; i++) {

    // do stuff

    if (i == 101) {
        break;
        // break jumps out of the loop once the condition is met
    }
}

// For loop using a continue

for (var i = 1; i < 10; i++) {
    // do stuff
    if (i % 5 == 0) {
        continue; // done with this iteration, not the entire loop, just this time around
    }
    // do second set of stuff
}


// [8] If Statements
/* --------------------------------------------- */

// Create a Basic Condition

var a = 1,
    b = 100;

if(a < b) {
    alert("a is less than b");
}


// Create Multiple Conditions

var time = new Date().getHours();

var morning = 10,
    afternoon = 20;

    if(time < morning) {
        //if condition 1 is true
        alert("Good Morning");
    } 
    else if (time < afternoon) {
        //if condition 2 is true
        alert("Good Afternoon");
    } 
    else {
        //if both condition are false
        alert("Good Night");
    }


// Ternary Condition

var now = new Date();
var greeting = "Good" + ((now.getHours() > 17) ? " evening." : " day.");

    //greeting = the test
    //evening = expression1 - wich is returned is the test is true
    //day = expression2 - wich is returned is the test is false

console.log(greeting);


// [9] JSON
/* --------------------------------------------- */

// Create JSON Object Key - Value Pairs

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

// How to parse the JSON object

    function createList() {

        var data = people.person;

        $.each(data, function(key, item) {

            var user = item.user,
                age = item.age,
                html = [];

            html.push('<p> + user + </p>');
            html.push('<p> + age + </p>');


            var build = html.join();

        });
    }

creatList(); // call function

console.log(createList);





// How to create a string

var str = "a b c";


// How to reverse the above string

var str = "a b c", //create the string
    len = str.length, //store it's length
    reverse = ""; // assign an empty string

for (var i = len; i >= 0; i--) {

    reverse += str[i]; // assign the results to reverse

}

var newStr = reverse; // store reverse as a new variable

console.log(newStr); // console the results


**[Back to top](#table-of-contents)**
