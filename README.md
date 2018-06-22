# Ionic Framework - A Deep Dive

## Pre-requesisits
- Node.js - v7.10.1
- NPM - v4.2.0
- Ionic - v3.20.0
- Cordova - 8.0.0
- VSCode
- XCode for Mac
- AndroidStudio 

##### Application Editor
Visual Studio Code - https://code.visualstudio.com

##### NodeJS and NPM
https://nodejs.org/download/release/v7.10.1/node-v7.10.1-x86.msi - Windows
https://nodejs.org/download/release/v7.10.1/node-v7.10.1.pkg - Mac

##### Ionic and Cordova
Open a command prompt (windows)/Terminal Window (mac/linux) and enter the following command. You may need add sudo in your mac/linux computer. -g stands for global and ionic and cordova will install in your global scope
```
$ npm install -g ionic cordova 
```
Now create a tabs based Hybrid Mobile Application using Ionic application using following 
```
$ ionic start ionic-deep-dive tabs
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
$ git add -A
$ git commit -m "Initial commit" --no-gpg-sign
```

## Testing App
You can test your application on browser, emulator/simulator or actual device.

### Testing on Browser
```
$ cd ionic-deep-dive/
$ ionic serve
```

Browse the url http://localhost:8100/ on your browser, normally default browser automatically opened.

### Add Platform
```
$ ionic cordova platform add ios
```

### Testing on Emulator/Simulate
You must have Emulator in working conditions, on windows Android SDK and Android Virtual Device must configure first or Android Studio installed, on Mac XCode installed. 

```
$ ionic cordova emulate
```

### Testing on Device
Testing device must connected with the computer using USB cable, any security or authentication must be allowed. For Android device you need to enable developer mode and USB debuging is turned on.

```
$ ionic cordova run
```

To get more help for run the following help command 

```
$ ionic cordova --help
```

#### Let's do some code clean up
- Open the project folder on VSCode 
  ```
  $ code .
  ```
  
- Navigate src/pages folder
- Delete about, contact and home folder (you may need some permision to edit/delete these files on Mac)
- From src/app folder, open app.module.ts -- there are some run-times error becasue of folder we just deleted. Remove these lines as well
- Again there is code error, remove these too.
- On src/tabs/tabs.ts - there are also some run times errors, we will update late just leave it as is.

### Ionic CLI Help
Don'f forget to the check it out, there are lots of commands available.
```
$ ionic --help
```

## Updating Application

The template application is ready and modify it with 4 tabs and each tab for following functions.

- Tab1 = Camera
- Tab2 = Barcode Scanner
- Tab3 = Torch light
- Tab4 = Media Player

### Add Tab Pages
Run the following comand and see the ionic magic
```
$ ionic generate page camera

$ ionic generate page Text2speech

$ ionic generate page torch

$ ionic generate page player
````
Now we four new folders src/pages, let's explore them and Remove the x.module.ts from each folder, we will use app.module.ts
Update <ion-title></ion-title>, Proper Camelcase Heading and also remove any unwanted comments if you want.
- camera
- Text2speech
- torch
- player

Once we remove x.module.ts, on each x.tx file, also remove @IonicPage annotation and IonicPage from import section. Now, let's update the tab.ts and tabs.html

##### tabs.ts
````
import { PlayerPage } from './../player/player';
import { TorchPage } from './../torch/torch';
import { Text2speech } from './../Text2speech/Text2speech';
import { CameraPage } from './../camera/camera';
import { Component } from '@angular/core';

@Component({
  templateUrl: 'tabs.html'
})
export class TabsPage {

  tab1Root = CameraPage;
  tab2Root = Text2speechPage;
  tab3Root = TorchPage;
  tab4Root = PlayerPage

  constructor() {

  }
}
``````

##### tabs.html
Ionic Icons @ https://ionicframework.com/docs/ionicons/ 
````
<ion-tabs>
  <ion-tab [root]="tab1Root" tabTitle="Camera" tabIcon="camera"></ion-tab>
  <ion-tab [root]="tab2Root" tabTitle="Text 2 Speech" tabIcon="barcode"></ion-tab>
  <ion-tab [root]="tab3Root" tabTitle="Torch" tabIcon="flash"></ion-tab>
  <ion-tab [root]="tab3Root" tabTitle="Player" tabIcon="play"></ion-tab>
</ion-tabs>
````

##### app.module.ts
```
import { PlayerPage } from './../pages/player/player';
import { Text2speech } from './../pages/Text2speech/Text2speech';
import { CameraPage } from './../pages/camera/camera';
import { NgModule, ErrorHandler } from '@angular/core';

......

 declarations: [
    MyApp,
    CameraPage,
    Text2SpeechPage,
    TorchPage,
    PlayerPage,
    TabsPage
  ]
  
 .......
 
 entryComponents: [
    MyApp,
    CameraPage,
    Text2SpeechPage,
    TorchPage,
    PlayerPage,
    TabsPage
  ],
  providers: [
    StatusBar,
    SplashScreen,
    {provide: ErrorHandler, useClass: IonicErrorHandler}
  ]
    
  `````

**_So far so good, please check it out on browser. Once you include the native function, you need to test on Emulator/Simulator or on device_**.

## Finishing Native Camera
Ionic Native Camera - https://ionicframework.com/docs/native/camera/
```
$ ionic cordova plugin add cordova-plugin-camera
$ npm install --save @ionic-native/camera
```
##### camera.ts
```
import { Component } from '@angular/core';
import { Camera } from '@ionic-native/camera';

@Component({
  selector: 'page-camera',
  templateUrl: 'camera.html',
})
export class CameraPage {

  public base64Image: string;
  constructor(private camera  : Camera) {

  }

  takePicture(){
    this.camera.getPicture({
          quality: 100,
          destinationType: this.camera.DestinationType.DATA_URL,
          encodingType: this.camera.EncodingType.JPEG,
          mediaType: this.camera.MediaType.PICTURE
      }).then((imageData) => {
      this.base64Image = this.base64Image = "data:image/jpeg;base64," + imageData; 
      console.log(imageData);
    })
  }
}
```
##### camera.html

```
.....

<ion-content padding>
  <ion-card>
    <ion-item>
      <img [src]="base64Image" *ngIf="base64Image" />
    </ion-item>
  </ion-card>

  <button ion-button (click)="takePicture()">Take Picture</button>
</ion-content>

```

#### app.module.ts
```
  .....
  
  providers: [
    StatusBar,
    SplashScreen,
    Camera
    {provide: ErrorHandler, useClass: IonicErrorHandler}
  ]
 ```


## Finishing Native Text to Speech
Text 2 Speech - https://ionicframework.com/docs/native/text-to-speech/
```
$ ionic cordova plugin add cordova-plugin-tts
$ npm install --save @ionic-native/text-to-speech
```

#### text2spech.html

```
<ion-content padding>
  <ion-list>
    <ion-item>
      
      <ion-textarea type="text" [(ngModel)]="text2Read" placeholder="Enter text to read"></ion-textarea>
    </ion-item>
  </ion-list>
  
  <button ion-button (click)="speak()">Speak</button>
</ion-content>
```

#### text2speech.ts
````
import { Component } from '@angular/core';
import { TextToSpeech } from '@ionic-native/text-to-speech';



@Component({
  selector: 'page-text2speech',
  templateUrl: 'text2speech.html',
})
export class Text2speechPage {

  text2Read: string;
  constructor(private tts: TextToSpeech) {
  }

  speak()
  {
    this.tts.speak(this.text2Read).then(() => console.log('Success')).catch((reason: any) => console.log(reason));
  }

  listen()
  {
    // TODO
    // Speech Recognition
  }
}
````

#### app.module.ts
```
  .....
  
  providers: [
    StatusBar,
    SplashScreen,
    TextToSpeech,
    Camera
    {provide: ErrorHandler, useClass: IonicErrorHandler}
  ]
 ```
 
## Finishing Native Flashlight
Flashlight - https://ionicframework.com/docs/native/flashlight/
```
$ ionic cordova plugin add cordova-plugin-flashlight
$ npm install --save @ionic-native/flashlight
```

#### torch.html
````
  <ion-content padding>
      <button ion-button (click)="on()">Turn On</button>
    <button ion-button (click)="off()">Turn Off</button>
     <button ion-button (click)="sos()">SOS On</button>
  </ion-content>
````

#### torch.ts
```
import { Component } from '@angular/core';
import { Flashlight } from '@ionic-native/Flashlight';

@Component({
  selector: 'page-torch',
  templateUrl: 'torch.html',
})
export class TorchPage {

  constructor(private flashlight: Flashlight) {
  }

  on()
  {
    this.flashlight.switchOn();
  }

  off(){
    this.flashlight.switchOff();
  }
  
   sos()
  {
    // TODO
    //three short flashes, three long flashes, three short flashes
  }
}
````

#### app.module.ts
````
........

providers: [
    StatusBar,
    Camera,
    TextToSpeech,
    Flashlight,
    SplashScreen,
    {provide: ErrorHandler, useClass: IonicErrorHandler}
  ]
````

## Finishing Native Media Player
Media - https://ionicframework.com/docs/native/media/
```
$ ionic cordova plugin add cordova-plugin-media
$ npm install --save @ionic-native/media
```

By now you are expert to develop mobile app using Ionic Framework. Let's continue and finish up.
