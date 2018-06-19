# Ionic Framework - A Deep Dive

## Pre-requesisits
- Node.js - v7.10.1
- NPM - v4.2.0
- Ionic - v3.20.0
- Cordova - 8.0.0
- VSCode

###### Application Editor
Visual Studio Code - https://code.visualstudio.com

###### NodeJS and NPM
https://nodejs.org/download/release/v7.10.1/node-v7.10.1-x86.msi - Windows
https://nodejs.org/download/release/v7.10.1/node-v7.10.1.pkg - Mac

###### Ionic and Cordova
Open a command prompt (windows)/Terminal Window (mac/linux) and enter the following command. You may need add sudo in your mac/linux computer. -g stands for global and ionic and cordova will install in your global scope
```
$ sudo npm install -g ionic cordova 
> npm install -g ionic cordova
```
Now create a tabs based Hybrid Mobile Application using Ionic application using following 
```
$ sudo ionic start ionic-deep-dive tabs
> ionic start ionic-deep-dive tabs
```
```
Would you like to integrate your new app with Cordova to target native iOS and
Android? (Y/n) Y
````
```
Install the free Ionic Pro SDK and connect your app? (Y/n) n
```

It will take few minutes to complete the process, and your skeleton application is ready to test. 

If you want put your source code to the git repo, please do so using following commands
```
$ sudo git add -A
$ sudo git commit -m "Initial commit" --no-gpg-sign

> git add -A
> git commit -m "Initial commit" --no-gpg-sign
```

## Testing App
You can test your application on browser, emulator/simulator or actual device.

Testing on Browser
```
$ cd ionic-deep-dive/
$ sudo ionic serve

> cd ionic-deep-dive/	
> ionic serve
```

Browse the url http://localhost:8100/ on your browser, normally default browser automatically opened.

## Add Platform
```
$ sudo ionic cordova platform add ios
> ionic cordova platform add android
```
## Testing on Emulator/Simulate
You must have Emulator in working conditions, on windows Android SDK and Android Virtual Device must configure first or Android Studio installed, on Mac XCode installed. 

```
$ sudo ionic cordova emulate
> ionic cordova emulate
```
## Testing on Device
Testing device must connected with the computer using USB cable, any security or authentication must be allowed. For Android device you need to enable developer mode and USB debuging is turned on.

```
$ sudo ionic cordova run
> ionic cordova run
```

To get more help for run the following help command 
```
$ sudo ionic cordova --help
> ionic cordova --help
```

The template application is ready and modify it with 4 tabs and each tab for following functions.

- Tab1 = Camera
- Tab2 = Barcode Scanner
- Tab3 = Torch light
- Tab4 = Media Player

Let's do come code clean up
- the project folder on VSCode.
- 

## Ionic CLI Help
Don'f forget to the check it out, there are lots of commands available.
```
ionic --help
```


