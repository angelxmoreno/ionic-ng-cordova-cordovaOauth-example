# ionic-ng-cordova-cordovaOauth-example
Attempting to make Ionic Framework + NG-Cordova and cordovaOauth play together


## Steps I followed:
```sh
$ node -v
v0.12.7

$ npm -v
2.14.2

$ cordova -v
5.3.1

$ ionic -v
1.6.4

$ ionic start myApp blank
Creating Ionic app in folder /Users/amoreno/Projects/InstaList/myApp based on blank project
Downloading: https://github.com/driftyco/ionic-app-base/archive/master.zip
[=============================]  100%  0.0s
Downloading: https://github.com/driftyco/ionic-starter-blank/archive/master.zip
[=============================]  100%  0.0s
Updated the hooks directory to have execute permissions
Update Config.xml
Initializing cordova project
Adding in iOS application by default
npm http GET https://registry.npmjs.org/cordova-ios
npm http 304 https://registry.npmjs.org/cordova-ios

Your Ionic project is ready to go! Some quick tips:
...

$ cd myApp/
$ ionic platform ls
Updated the hooks directory to have execute permissions
Installed platforms: ios 3.8.0
Available platforms: amazon-fireos, android, blackberry10, browser, firefoxos, osx, webos

$ ionic platform update ios
Updated the hooks directory to have execute permissions
Updating ios project...
iOS project updated with cordova-ios@3.9.1
Running command: /Users/amoreno/Projects/InstaList/myApp/hooks/after_prepare/010_add_platform_class.js /Users/amoreno/Projects/InstaList/myApp
add to body class: platform-ios

$ ionic serve -lc
Running live reload server: http://localhost:35729
Watching : [ 'www/**/*', '!www/lib/**/*' ]
Running dev server: http://localhost:8100
Ionic server commands, enter:
  restart or r to restart the client app from the root
  goto or g and a url to have the app navigate to the given url
  consolelogs or c to enable/disable console log output
  serverlogs or s to enable/disable server log output
  quit or q to shutdown the server and exit
  
$ ionic run ios
...
```

At this point the app runs with no errors in the browser nor in the ios emulator.

```sh
$ bower install ngCordova
bower cached        git://github.com/driftyco/ionic-bower.git#1.1.0
...
```
Running bower deletes many files in the `www/lib` and adds what i assume to be, newer versions:

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    www/lib/ionic/js/angular-ui/angular-ui-router.js
	deleted:    www/lib/ionic/js/angular-ui/angular-ui-router.min.js
	deleted:    www/lib/ionic/js/angular/angular-animate.js
	deleted:    www/lib/ionic/js/angular/angular-animate.min.js
	deleted:    www/lib/ionic/js/angular/angular-resource.js
	deleted:    www/lib/ionic/js/angular/angular-resource.min.js
	deleted:    www/lib/ionic/js/angular/angular-sanitize.js
	deleted:    www/lib/ionic/js/angular/angular-sanitize.min.js
	deleted:    www/lib/ionic/js/angular/angular.js
	deleted:    www/lib/ionic/js/angular/angular.min.js
	modified:   www/lib/ionic/scss/_reset.scss
	modified:   www/lib/ionic/scss/ionicons/_ionicons-font.scss
	modified:   www/lib/ionic/scss/ionicons/_ionicons-icons.scss
	modified:   www/lib/ionic/scss/ionicons/_ionicons-variables.scss
	modified:   www/lib/ionic/scss/ionicons/ionicons.scss
	deleted:    www/lib/ionic/version.json

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	www/lib/angular-animate/
	www/lib/angular-sanitize/
	www/lib/angular-ui-router/
	www/lib/angular/
	www/lib/ionic/.bower.json
	www/lib/ionic/README.md
	www/lib/ionic/bower.json
	www/lib/ionic/scss/_loaders.scss
	www/lib/ionic/scss/_split-pane.scss
	www/lib/ionic/scss/ionicons/_ionicons-animation.scss
	www/lib/ngCordova/
```
Running `ionic serve -lc` and `ionic run ios` still run with no errors. 
	
As per the instructions on ngcordova.com
```
Include ng-cordova.js or ng-cordova.min.js in your index.html file before cordova.js and after your AngularJS / Ionic file (since ngCordova depends on AngularJS).
```
I modify my index.html file to look like so:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, width=device-width">
    <title></title>

    <link href="lib/ionic/css/ionic.css" rel="stylesheet">
    <link href="css/style.css" rel="stylesheet">

    <!-- IF using Sass (run gulp sass first), then uncomment below and remove the CSS includes above
    <link href="css/ionic.app.css" rel="stylesheet">
    -->

    <!-- ionic/angularjs js -->
    <script src="lib/ionic/js/ionic.bundle.js"></script>

    <!-- adding ngCordova before cordova.js and after Angular -->
    <script src="lib/ngCordova/dist/ng-cordova.js"></script>

    <!-- cordova script (this will be a 404 during development) -->
    <script src="cordova.js"></script>

    <!-- your app's js -->
    <script src="js/app.js"></script>
  </head>
  <body ng-app="starter">

    <ion-pane>
      <ion-header-bar class="bar-stable">
        <h1 class="title">Ionic Blank Starter</h1>
      </ion-header-bar>
      <ion-content>
      </ion-content>
    </ion-pane>
  </body>
</html>
```
Next I include ngCordova as a dependency in my angular app module like so:

```js
// Ionic Starter App

// angular.module is a global place for creating, registering and retrieving Angular modules
// 'starter' is the name of this angular module example (also set in a <body> attribute in index.html)
// the 2nd parameter is an array of 'requires'
angular.module('starter', ['ionic', 'ngCordova'])

.run(function($ionicPlatform) {
  $ionicPlatform.ready(function() {
    // Hide the accessory bar by default (remove this to show the accessory bar above the keyboard
    // for form inputs)
    if(window.cordova && window.cordova.plugins.Keyboard) {
      cordova.plugins.Keyboard.hideKeyboardAccessoryBar(true);
    }
    if(window.StatusBar) {
      StatusBar.styleDefault();
    }
  });
})

```
Running `ionic serve -lc` and `ionic run ios` still run with no errors. 

Next I include the plugin:

```sh
$ cordova plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-inappbrowser.git 
Fetching plugin "https://git-wip-us.apache.org/repos/asf/cordova-plugin-inappbrowser.git" via git clone
Repository "https://git-wip-us.apache.org/repos/asf/cordova-plugin-inappbrowser.git" checked out to git ref "master".
Installing "cordova-plugin-inappbrowser" for ios
```

I then add a controller to my app:

```js
.controller('MyCtrl', function($scope, $cordovaOauth) {
    $scope.instagramLogin = function() {
        $cordovaOauth.instagram("CLIENT_ID_HERE", []).then(function(result) {
           console.info('results', results);
        }, function(error) {
            console.info('error', error);
        });
    };
    
});

```

I then attach the controller to my index.html `<ion-content />` and create a button to run `$scope.instagramLogin()`:

```html
<ion-pane>
  <ion-header-bar class="bar-stable">
    <h1 class="title">Ionic Blank Starter</h1>
  </ion-header-bar>
  <ion-content ng-controller="MyCtrl">
  	<button ng-click="instagramLogin()" class="button button-block button-positive">
    	Log In with Instagram
  	</button>
  </ion-content>
</ion-pane>
```

At this point, running the app via `ionic serve` will throw a warning when clicking the button. 

