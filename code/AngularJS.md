# AngularJS


## Setting up your main app file (app.js)

**Note:** Order matters! app.js needs to be included before any other non-vendor files.

```
1. angular.js
2. app.js
3. controller.js (ext)


*** Markup View ***

	<!-- build:js js/vendor.js -->
    <script src="bower_components/angular/angular.js"></script>

    <!-- build:js js/app.js -->
    <script src="js/app.js"></script>
    <script src="js/main/controller.main.js"></script>
    <script src="js/info/controller.info.js"></script>
    

```

**Assign 'AppName' to a variable to be used accross the application.**

**Note:** The below structure supports minification


```

var appName = angular.module('AppName',
    [
        'dependencyOne', //inject app dependency here (if needed)
        'dependencyTwo'
    ]
);


```


## AngularJS .controller

**Creating the Controller**

- Notice how we passed the variable $scope as a parameter to the controller function.
- appName.controller - assigns ModalController to AppName


```
appName.controller('ModalController', ['$scope',
    function($scope) {
        //assigning all varaibles to the $scope, makes them available within the containing element the controller is assigned to (in the html) 

        $scope.message = 'So, that\'s how scope works!';

        console.log(message); //should return the above string
    }
]);

```
 

## AngularJS .factory


**Creating a Factory Object**

- More re-useable and easier to maintain
- ModalFactory is the factory object

```
appName.factory('ModalFactory', [

    function() {

        return {

            //let's assign a true/false property to the NameFactory object

            modalStatus: false,
            //sets the default value to false (this property will be used to check the status of a bool value)


            getModalStatus: function() {
                return this.modalStatus;
                //get the status of modalStatus (can be true or false), and return it to modalStatus above

            },

            setModalStatus: function(status) {
                this.modalStatus = status;
                //here we are passing a parameter named 'status' and assigning it to modalStatus
            }
        };
    }
]);

```

**Now I can pass the above factory object to a controller, and leverage the properties inside it like so...**

```
appName.controller('ModalController', ['$scope', 'ModalFactory',

    function($scope, ModalFactory) {

        //let's create an event handler that toggles the true/false value

        $scope.openModel = function() {

            NameFactory.setModalStatus(true); //this updates the modalStatus to true

            $scope.showModal = ModalFactory.getModalStatus(); //watches and updates the status each time the event is triggered

        };
    }
]);

```


## Service Vs Factory


```
app.service('SomeService', function);
app.factory('SomeFactory', function);

```

**Spoiler alert:** Both are services!

Both are singleton objects (otherwise known as stateless objects) that contain useful functions that carry out specific task. Services are responsible for holding the business logic. Keeping that logic outside of your controller is important. A controller is only responsible for binding modal data to views using $scope. It should not contain logic to fetch data or manipulate it.

The main difference between the two is in the way we reference thier methods.

### AngularJS .service

Notice: how we create service methods using `this.methodname`.

```
app.service('SomeService', [
	function() {
		this.method1 = function() {
			//some code
		}
		this.method2 = function() {
			//some code
		}	
	}
]);

// When declaring 'SomeService' as an injectable argument, you will be provided with an instance of the function. 

```

### AngularJS .factory

Notice: how we created an object named `'factory'` and assigned our methods to it, then returned that object so it is accessible when passed as an injectable argument through the 'SomeFactory' object. 

```
app.factory('SomeFactory', [
	function() {
	
		var factory = {};
	
		factory.method1 = function() {
			//some code
		}
		
		factory.method2 = function() {
			//some code
		}
		
		return factory	
		
	}
]);

// When declaring 'SomeFactory' as an injectable argument, you will be provided with the value that is returned by invoking the function reference passed to app.factory.

```

**Why use either?**
 
- First it fulfills the principle of separation of concern and/or segregation of duties. Each component is responsible for it's own work. 
- Second, it make each component more testable.


<br /></br />
## AngularJS .directives

**Why Use?**

Let's say you have a template that is repeated many times in your code. When you change it in one place, you would have to change it in several others. This is a good opportunity to use a directive to simplify your template – making the app easy scalable and maintainable.

**When to use directives?**

- If you have a reusable HTML component
```
<ui-widget>
```

- If you want reusable HTML behavior
```
<div ng-click="...">
```

- If you want to wrap a jQuery plugin
```
<div ui-date></div>
```

- Almost anytime you need to interface with the DOM
    - Typically it's back practice to interact with the DOM anywhere else (i.e. Controllers, Services, ect). The reason being, it makes your code less testable and more coupled to the DOM  

**Things to note:**

- If you plan on using the same directive multiple times and you don't isolate the scope, you're going to do something called 'Polluting' the scope of the parent.


**Scope:** Three trypes of isolate scope

- number: "@" | Used for reading an attribute

```
 <div number="555-1234"></div> (555-1234 being the attribute)
 
```

- network: "=" | Used for creating a bi-directional two way binding (updates done within the directive, also update within the controller scope)

```
 <div network="network"></div> (network being the selector bound to the controller)

```

- makeCall: "&" | Used to make a call on something in the controller scope

```
 <div make-call="leaveVoicemail(number, message)"></div> (example below)

```

**Declaration Styles:** Options for directive declaration usage

```
E = element | <my-menu title="Products"> Some Code </my-menu> 

A = attribute | <div my-menu="Products"> Some Code </my-menu> 

C = class | <div class="my-menu:Products"> Some Code </my-menu>

M = comment | <!-- directive: my-menu Products -->  


```

**Definition Options:**

Using a basic pseudo-code template good for creating any directive...

```

var appName = angular.module('AppName', [...]);

appName.directive('appNameDirectiveName',
    function() {
        return {
            restrict: 'E',                              # See above Declaration Styles
            scope: {},                                  # Create a new scope for the directive rather than inheriting the parent scope
            replace: true,                              # If true, replace the current element. If false or unspecified, append this directive to the current element
            transclude: true,                           # Lets you move the original children of a directive to a location inside the new template
            templateUrl: 'path/to/template.html',       # Specify tfhe template to be loaded by URL
            link: function(scope, element, attrs) {     # Programmatically modify resulting DOM element instances, add event listeners, and set up data binding
                scope.showStuff = false;
                scope.toggleStuff = function toggle() {
                    scope.showStuff = !scope.showStuff;
                }              
            }
        }
    }
);

```

## Helpful Hints:


##### Notes on Dependencies:

- Make sure all css and js files are included in the index.html file during development. If you're getting error's in your network tab, I've found that to be a good starting point.
	

##### Notes on Custom Directives: 


Naming conventions matter!

**JS files:** Your directives name should be camel case.
 
```
customDirective

```
	
**HTML files:** Your directives name should be lower based and seperated using hyphens.

```	
custom-directive

or

custom-directive="attr-name"
```

**Directives - Templating Issues

If you encounter the following...

```
Error: error:tplrt Invalid Template Root
Template for directive '{0}' must have exactly one root element. {1}

```

And your directive is declaring a template (or templateUrl) and replace mode is on (replace: true), then your directives template probably looks something like this...

```
<div class="container">
    <!-- some code -->
</div>
<div class="container">
    <!-- some code -->
</div>

```

Angulars replacement operation results in a single element (the directive) being replaced. The replacment of multiple elements or nodes is unsupported (in v1.3) and not commonly needed in practice.

To correct this, you have two options.

* Move all sibling elements into one parent element.

```
<div class="container-wrap">
    <div class="container">
        <!-- some code -->
    </div>
    <div class="container">
        <!-- some code -->
    </div>
</div>
```

* Change the rescrict option to and attribute instead of an element.

**JS:**
```
appName.directive('custom',
    function() {
        return {
            restrict: 'A'                     
        }
    }
);

```
**HTML:** (partial template)

```
<div class="container-wrap" custom>
    <!-- Directive template pulled in here -->
</div>

```



