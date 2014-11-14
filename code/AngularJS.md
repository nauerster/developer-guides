# AngularJS



###AngularJS App File
*****
**Setting the app file up (app.js)**

**Note:** app.js needs to be included before any other file

```
1. angular.js
2. app.js
3. controller.js (ext)
```

**Assign AppName to a variable to be used accross the application.**

**Note:** The below structure supports minification

```
var appName = angular.module('AppName',
    [
        'dependencyOne', //inject app dependency here (if needed)
        'dependencyTwo'
    ]
);

```

<br /><br />
###Controllers
****

**Creating the Controller**

- Notice how we passed the variable $scope as a parameter to the controller function
- appName.controller - assigns NameController to AppName



```
appName.controller('NameController', ['$scope',
    function($scope) {
        //assigning all varaibles to the $scope, makes them available within the containing element the controller is assigned to (in the html) 

        $scope.message = 'So, that\'s how scope works!';

        console.log(message); //should return the above string
    }
]);

```

<br /><br />
###Factories
****

**Creating a Factory Object**

- More re-useable and easier to maintain
- NameFactory is the factory object

```
appName.factory('NameFactory', [

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

**Now I can pass the above the factory object to a controller, and leverage the properties inside it like so...**

```
appName.controller('ModalController', ['$scope', 'NameFactory',

    function($scope, NameFactory) {

        //let's create an event handler that toggles the true/false value

        $scope.openModel = function() {

            NameFactory.setModalStatus(true); //this updates the modalStatus to true

            $scope.showModal = NameFactory.getModalStatus(); //watches and updates the status each time the event is triggered

        };
    }
]);

```




