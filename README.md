# Ionic Framework - A Deep Dive

## Pre-requesisits
- Node.js - v7.10.1
- NPM - v6.0.1
- Ionic - v3.20.0
- Cordova - 8.0.0

Let’s install/update your system as mentioned in the pre-requisites.

NodeJS and NPM

(https://nodejs.org/download/release/v7.10.1/node-v7.10.1-x86.msi) - Windows
(https://nodejs.org/download/release/v7.10.1/node-v7.10.1.pkg) - Mac

Ionic and Cordova

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
Android? Y
````
```
Install the free Ionic Pro SDK and connect your app? (Y/n) n
```

If you want put your source code to the git repo, please do so using following commands
```
$ sudo git add -A
$ sudo git commit -m "Initial commit" --no-gpg-sign

> git add -A
> git commit -m "Initial commit" --no-gpg-sign
```

// Create a new project
$ ionic start meetup-demo tabs

// Run app in Browser
$ ionic serve

// let select your platform
$ ionic platform add iOS

// build app
$ ionic build ios

// run your app simulator or device
// if a mobile device is connected app will run on the // device, if not it will try to find out simulator
$ ionic run

