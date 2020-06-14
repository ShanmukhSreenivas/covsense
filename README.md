# CovSense
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/3b0fa4c8276e4721b145e75be5ad3b5b)](https://app.codacy.com/manual/saivittalb/covsense?utm_source=github.com&utm_medium=referral&utm_content=saivittalb/covsense&utm_campaign=Badge_Grade_Dashboard)
[![Version](https://badge.fury.io/gh/saivittalb%2Fcovsense.svg)](https://badge.fury.io/gh/saivittalb%2FCovsense)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![PR's Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](http://makeapullrequest.com) 
 

<p align="center"><img src="https://firebasestorage.googleapis.com/v0/b/poised-elf-275018.appspot.com/o/logo.png?alt=media&token=80d1d621-b2cc-4a0d-8672-b6da83485d86" height="300" width="300"></p> 

An Android based contact tracing app which enables people to self-isolate if they have been in close proximity to someone tested positive for COVID-19. The app uses a combination of Wi-Fi, Bluetooth, BluetoothLE and ultrasonic modem to communicate a unique-in-time pairing code between devices (using the Nearby Messages Google API). This technology can be scaled beyond the demo to work on iOS as well. Furthermore the solution can be embedded in other existing applications as a library to have larger adoption of the contact tracer.

Available in Dark and Light themes. Themes are pre-chosen depending on the user system settings. Preview of the app is available below in this document. 

## License
This project is licensed under the Apache License 2.0, a permissive license whose main conditions require preservation of copyright and license notices. Contributors provide an express grant of patent rights. Licensed works, modifications, and larger works may be distributed under different terms and without source code. Trademark use is also strictly prohibited. Any material found which vandalises or threatens any sort of plagiarism will be strictly given a legal action.


## Preview

### Dark theme 
<p align="center"><img src="https://firebasestorage.googleapis.com/v0/b/poised-elf-275018.appspot.com/o/DarkThemeScreens.png?alt=media&token=c257b467-c5b9-42a4-89d3-ea5a27f72784"></p> 

### Light theme
<p align="center"><img src="https://firebasestorage.googleapis.com/v0/b/poised-elf-275018.appspot.com/o/LightThemeScreens.png?alt=media&token=ebcd46f2-7a91-4231-a070-0fa7cfd2379e"></p> 

## Android Signed APK build (Debug)
The signed ```.apk``` debug build variant of this app that you can install on your Android device is available here in the link below. \
https://firebasestorage.googleapis.com/v0/b/poised-elf-275018.appspot.com/o/app-debug.apk?alt=media&token=e59d898b-7f66-4055-9a21-48a11fef1e37

## Demo
A short video demonstration of the app when the health status of one user has been modified is available here in the links below.\
https://youtu.be/G6MQR8V4Wig \
https://firebasestorage.googleapis.com/v0/b/poised-elf-275018.appspot.com/o/CovSense%20-%20Android%20Demo.mp4?alt=media&token=d0f71f6a-6a29-415a-8099-7e64fd5d6f40

## Corner cases (known as of now)
- Tracking does not happen when the user is on a phone call.

If you discover any failing test cases, you are encouraged to open an issue or a PR regarding it. 

## Working
After you sign in, you get an OTP generated using Firebase Phone Authentication. After you login, the application starts a background service that constantly publishes and receives the Firestore Database UIDs, by using the Nearby Messages API from Google. When two devices are in close proximity (approximately 4 metres to 5 metres for Bluetooth + Sonar) their meetup is registered in Firestore.

In the logged in screen, you can choose your current health status and press the button. This updates your health status in the database. Using Firestore Cloud Messages, there is a JavaScript function that triggers when this update happens and sends a push notification to the users that you have interacted with. 

## Components
- Android codebase in Java 
- Firebase Authentication   (authenticate requests)
- Firestore                 (database)
- Nearby Messages API       (contact tracing)
- Firebase Functions        (serverless code)

###### Note 
Developed with Android Studio version 3.6.3.

## Installation
### Prerequisites
- Before you begin, make sure your development environment includes [Node.js®](https://nodejs.org/), [yarn](https://classic.yarnpkg.com/) and [npm](https://www.npmjs.com) package managers.
- Download [Android Studio](https://developer.android.com/studio).
- Also make sure to create [Google Developers Console](https://console.developers.google.com), [Google Cloud Platform](https://console.cloud.google.com), and [Firebase](https://firebase.google.com) accounts for generating necessary API keys and setting up the project. 

### Android app configuration
- Follow the instructions for setting up your [Google Maps SDK for Android](https://developers.google.com/maps/documentation/android-sdk/start).
- Follow the instructions for interacting with the [Google Nearby Messages API](https://developers.google.com/nearby/messages/android/get-started).
- Update your app module <b>build.gradle</b> file with
    - The <b>API_KEY</b> for the Nearby Messages API, ```API_KEY = "\"YOUR_API_KEY_HERE\""```.
    - The <b>MAPS_API_KEY</b> for the Google Maps SDK for Android, ```MAPS_API_KEY = "\"YOUR_MAPS_API_KEY_HERE\""```.  
- Update your <b>AndroidManifest.xml</b> file in maps meta data with your <b>API_KEY</b>, ```value = "YOUR_MAPS_API_KEY_HERE"```.
- Go to your Firebase console, setup this project, select Android app, add the package name of this app and download <b>google-services.json</b>.
- Move the <b>google-services.json</b> file you just downloaded into your Android app module root directory.
- Create a <b>gradle.properties</b> file in the project's root directory and enter the following lines.
```
android.useAndroidX=true
android.enableJetifier=true
```

### Database configuration
- In the Firebase console, open the Authentication section.
- On the Sign-in Method page, enable the Phone Number sign-in method.
- Follow the installation guide for [Firestore](https://firebase.google.com/docs/firestore/quickstart).
- Set up [Firebase Functions](https://firebase.google.com/docs/functions/get-started).
- Once you complete the Firebase Functions setup, open terminal/console window over the project directory and run following commands.
```bash
$ cd ./firestore/functions

$ yarn

$ npm install

$ cd ..
 
$ firebase deploy --only functions
```

### JSON schema for Firebase
Two tables named <b>users.json</b> and <b>users-meetings.json</b> are pre-saved in the `./CovSense/firestore` directory.
    
## Contributing
- Fork this project by clicking the ```Fork``` button on top right corner of this page.
- Open terminal/console window. 
- Clone the repository by running following command in git:
 ```bash
$ git clone https://github.com/[YOUR-USERNAME]/covsense.git
```
- Add all changes by running this command.
```bash
$ git add .
```
- Or to add specific files only, run this command.
```bash
$ git add path/to/your/file
```
- Commit changes by running these commands.
```bash
$ git commit -m "DESCRIBE YOUR CHANGES HERE"

$ git push origin
```
- Create a Pull Request by clicking the ```New pull request``` button on your repository page.

