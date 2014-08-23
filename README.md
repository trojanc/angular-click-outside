angular-click-outside
=====================

An angular directive to detect a click outside of an elements scope. Great for closing dialogues, drawers and off screen menu's etc.

###Usage

To use this directive, ensure the element you want to detect a close outside of has an id (not class) assigned. Id's are needed as multiple elements may have the same class. Add the directive via the `click-outside` attribute, and give exceptions via the `outside-if-not` attribute.

Basic example:
    
    <div class="menu" id="main-menu" click-outside="closeThis">
        ...
    </div>
    
This is of little use though without a callback function to do something with that click:
	
    <div class="menu" id="main-menu" click-outside="closeThis()">
        ...
    </div>
	
Where `closeThis()` is the function assigned to the scope via the controller such as:

    angular
        .module('myApp')
        .controller('MenuController', ['$scope', MenuController]);
        
    function MenuController($scope) {
        $scope.closeThis = function () {
            console.log('closing');
        }
    }
    
    <button id="my-button">Menu Trigger Button</button>
    <div ng-controller="MenuController">
        <div class="menu" id="main-menu" click-outside="closeThis()" outside-if-not="my-button">
            ...
        </div>
    </div>

###Adding Exceptions
You can also add exceptions via the `outside-if-not tag`, which executes the callback function, but only if the id's listed wasn't clicked. In this case `closeThis()` will be called only if clicked outside _and_ #my-button wasn't clicked as well. This can be great for things like slide in menus that might have a button outside of the menu scope that triggers it:
    
    <button id="my-button">Menu Trigger Button</button>
    <div class="menu" id="main-menu" click-outside="closeThis()" outside-if-not="my-button">
        ...
    </div>
	
You can have more than one exception by comma delimiting a list such as:
	<button id="my-button">Menu Trigger Button</button>
    <div class="menu" id="main-menu" click-outside="closeThis()" outside-if-not="my-button, another-button">
        ...
    </div>
	<button id="another-button">A second trigger button</button>
