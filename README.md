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



```

ionic build ios

```
