### Which platform(s) does your issue occur on?
- Android
- Target: Android 7.0. API: 24
- Emulator. Pixel 2 API 24

### Please, provide the following version numbers that your issue occurs with:
```
$ tns --version
5.4.2
```
- Cross-platform modules: `"version": "5.2.2"`
(check the 'version' attribute in the `node_modules/tns-core-modules/package.json` file in your project)

- Runtime(s): `"version": "5.2.0"`
(look for the `"tns-android"` and `"tns-ios"` properties in the `package.json` file of your project)

- Plugin(s): (look for the version numbers in the `package.json` file of your project and paste your dependencies and devDependencies here)

```
    "dependencies": {
        "@angular/animations": "~7.2.0",
        "@angular/common": "~7.2.0",
        "@angular/compiler": "~7.2.0",
        "@angular/core": "~7.2.0",
        "@angular/forms": "~7.2.0",
        "@angular/http": "~7.2.0",
        "@angular/platform-browser": "~7.2.0",
        "@angular/platform-browser-dynamic": "~7.2.0",
        "@angular/router": "~7.2.0",
        "nativescript-angular": "~7.2.1",
        "nativescript-oauth2": "^2.2.2",
        "nativescript-theme-core": "~1.0.4",
        "reflect-metadata": "~0.1.12",
        "rxjs": "~6.3.0",
        "tns-core-modules": "~5.2.0",
        "zone.js": "~0.8.26"
    },
    "devDependencies": {
        "@angular/compiler-cli": "~7.1.0",
        "@nativescript/schematics": "~0.5.0",
        "@ngtools/webpack": "~7.1.0",
        "nativescript-dev-typescript": "~0.8.0",
        "nativescript-dev-webpack": "~0.20.0"
    },
```

### Please, tell us how to recreate the issue in as much detail as possible. 

```
$ git clone https://github.com/napolev/nativescript-oauth2-issue
$ cd nativescript-oauth2-issue/demo-angular
$ npm i
$ tns platform clean android
$ tns devices
$ tns run android [--device <device-id>]
```
Once the app is running on the phone:
1. login with any Google account
2. you will see the access token on the console
3. logout
4. login again
5. you will see some errors on the console from now on any subsequent logins


### Is there any code involved? 

Preview: https://www.youtube.com/watch?v=T-6qj1SAsnk

Github repo: https://github.com/napolev/nativescript-oauth2-issue

I think the problem is on the following file:

/demo-angular/node_modules/nativescript-oauth2/tns-oauth-login-sub-controller.js

![Preview](https://i.ibb.co/Bgh3vmn/image.png)

where after the first login/logout, when trying to login again, the variable: `this.authState` is `null` and it is getting asked for: `this.authState.loginCompletion` which throws the exception:

```
Unhandled Promise rejection: Cannot read property 'loginCompletion' of null ;
Zone: <root> ; Task: Promise.then ; Value: TypeError:
Cannot read property 'loginCompletion' of null TypeError: Cannot read property 'loginCompletion' of null
```
