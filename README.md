[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Codecov Coverage](https://img.shields.io/codecov/c/github/NewBieBR/typescript-react-native-starter.svg?style=popout)](https://codecov.io/gh/NewBieBR/typescript-react-native-starter)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)

# Typescript React Native Starter

This is an opionated configuration for typescript react native project.

## Features

- **Typescript**
  - [React Native's typescript template](https://github.com/react-native-community/react-native-template-typescript) based

- **Flux State management**
  - [Redux](https://github.com/reduxjs/redux): predictable state container
  - [Redux Persist](https://github.com/rt2zz/redux-persist): offline store
  - [typesafe-actions](https://github.com/piotrwitek/typesafe-actions): create typesafe actions easily

      ```javascript
      import { action } from 'typesafe-actions';
      import * as types from './actionTypes';

      export const myAction = payload => action(types.MY_ACTION_TYPE, payload);
      ```

  - [Redux Saga](https://github.com/redux-saga/redux-saga): side effect model for Redux

- **Navigation**
  - [React Navivation](https://github.com/react-navigation/react-navigation): easy-to-use navigation solution based on Javascript

- **Unit testing**
  - Unit tests with [Jest](https://github.com/facebook/jest), [Enzyme](https://github.com/airbnb/enzyme) and [react-native-testing-library](https://github.com/callstack/react-native-testing-library)
- - [Codecov](https://codecov.io/): coverage report

- **CI/CD**

  - Run linting pre-commit and unit testing pre-push with [husky](https://github.com/typicode/husky)'s hooks
  - Placeholder App Icon: useful for uploading your app to beta quickly with Fastlane
  - [App Icon generator](https://github.com/dwmkerr/app-icon#readme): generate all required sizes, label and annotate icon.
  - Placeholder feature graphic and screenshot to upload beta android app quickly

- **Linting**
  - Tslint configured with Airbnb styles
  - Vscode Prettier compatible

- **Internationalization and localization**
  - [react-native-localization](https://github.com/stefalda/ReactNativeLocalization): easy to use package for i18n

- **Others**
  - [React Native Normalize](https://github.com/NewBieBR/react-native-normalize): make your app responsive easily
  - [Cocoapods](https://github.com/CocoaPods/CocoaPods): iOS dependencies manager
  - [jetifier](https://github.com/mikehardy/jetifier#readme): transition tool for [React Native 0.60 AndroidX migration](https://facebook.github.io/react-native/blog/2019/07/03/version-60#androidx-support)
  - [autobind-decorator](https://github.com/andreypopp/autobind-decorator#readme): bind your component's functions easily with a decorator

    Before:
    ```JSX
    handleClick()  {...}

    <button onClick={ this.handleClick.bind(this) }></button>
    ```
    After:
    ```JSX
    @boundMethod
    handleClick() {...}

    <button onClick={ this.handleClick }></button>
    ```

## Project Structure

```
├── __tests__                            // Unit tests
│   ├── App.test.tsx                     // App component's tests
│   ├── components
│   │   └── MyComponent.test.txs
│   └── ...
├── android
├── app.json
├── assets                               // All assets: images, videos, ...
├── index.js
├── ios
├── publishing                           // Icon, screenshots, preview,... for App Store & Play Store
└── src
    ├── App.tsx
    ├── actions                          // Actions
    │   ├── actionTypes.ts               // Action types
    │   └── app.ts                       // appReducer's actions
    ├── components                       // Components
    │   └── MyComponent.tsx
    ├── constants                        // Colors, sizes, routes,...
    │   └── strings.ts                   // i18n
    ├── containers                       // Screens, pages,...
    ├── lib                              // Libraries, services,...
    ├── index.tsx                        // Root component
    ├── reducers                         // Reducers
    │   └── app.ts                       // appReducer
    ├── sagas                            // Redux sagas
    ├── store.ts
    ├── types                            // Type declarations
    │   └── index.d.ts
    └── utils                            // Utilities
```

## Installation

- Clone this repo
  ```
  git clone git@github.com:NewBieBR/typescript-react-native.git <PROJECT_NAME>
  ```
  ```
  cd <PROJECT_NAME>
  ```
- Execute the installtion script
  ```
  ./bin/install.sh <PROJECT_NAME>
  ```

#### if (you want to use Codecov) {
- [Link your github repository with Codecov](https://docs.codecov.io/docs)

- Update your project's informations and the Codecov token `scripts` > `codecov` in `package.json`

#### } else {
- Change `husky` > `pre-push` to `yarn test` in `package.json`
#### }
## Manual Installation

- Clone this repo

  ```
  git clone git@github.com:NewBieBR/typescript-react-native.git <PROJECT_NAME>
  ```

  ```
  cd <PROJECT_NAME>
  ```

- Install dependencies
  ```
  yarn
  ```
- Rename the project

  ```
  yarn run rename <PROJECT_NAME>
  ```

- Migrate to AndroidX to [support React Native 0.60](https://facebook.github.io/react-native/blog/2019/07/03/version-60#androidx-support)

  ```
  yarn jetify
  ```

- Update pods

  ```
  cd ios && pod install
  ```

- Remove .git

  ```
  rm -rf .git
  ```

#### if (you want to use Codecov) {
- [Link your github repository with Codecov](https://docs.codecov.io/docs)

- Update your project's informations and the Codecov token `scripts` > `codecov` in `package.json`

#### } else {
- Change `husky` > `pre-push` to `yarn test` in `package.json`
#### }

## Note

### Responsiveness with React Native Normalize

Use the **normalize** functio from react-native-normalize whenever you have to use a *hard value* (100, 200, 1000,...). This function will adapt your value accordingly to different screen sizes

### Without `normalize`
![](https://i.imgur.com/bLbnjsC.jpg)

### With `normalize`
![](https://i.imgur.com/4IqqAR2.jpg)


### NavigationService

You can [navigate without navigation prop](https://reactnavigation.org/docs/en/navigating-without-navigation-prop.html) by using **NavigationService** from `src/lib/NavigationService.ts`

```typescript
import NavigationService from '../lib/NavigationService';

//...

NavigationService.navigate('ChatScreen', { userName: 'Lucy' });
```

### Cocoapod

When you run `react-native link` and the linked library has podspec file, then the linking will use Podfile. To disable this feature, remove

```ruby
# Add new pods below this line
```

from line 24 in `ios/Podfile`

### Static bundle

The static bundle is built every time you target a physical device, even in Debug. To save time, the bundle generation [is disabled in Debug](https://facebook.github.io/react-native/docs/running-on-device)


### react-native-screens

You can use react-native-screens with react-navigation in order to [improve memory consumption](https://reactnavigation.org/docs/en/community-libraries-and-navigators.html#react-native-screens)

- Install and follow steps in `Usage with react-navigation (without Expo)` from [react-native-screens](https://github.com/kmagiera/react-native-screens)

- Open `./src/index.tsx` and uncomment

```javascript
// import { useScreens } from 'react-native-screens';
// useScreens();
```


### Beta distribution with Fastlane
- Install [fastlane](https://docs.fastlane.tools/getting-started/ios/setup/)
  ```bash
  # Using RubyGems
  sudo gem install fastlane -NV

  # Alternatively using Homebrew
  brew cask install fastlane
  ```

#### iOS
- Open your project Xcode workspace and update your app's `Bundle Identifier` and `Team`
- Initialize fastlane
  ```bash
  cd <PROJECT_NAME>/ios
  fastlane init
  ```
- Distribute your app
  ```bash
  fastlane beta
  ```

#### Android
- [Collect your Google Credentials](https://docs.fastlane.tools/getting-started/android/setup/#collect-your-google-credentials)
- Open your project with Android Studio and update your app's `applicationId` in `build.gradle (Module: app)` file
- Select `Generated Signed Bundle / APK...` from the `Build` menu
- `Next` then `Create new...` under `Key store path` then `Next` and `Finish`
- The first time you deploy your application, you MUST upload it into Google Play Console manually. Google don't allow to use theirs APIs for the first upload.
- Create your application in the [Google Play Console](https://play.google.com/apps/publish/) (unlike for iOS Fastlane cannot do that for you)
- Make sure that these 4 checkmark icons are green
    > Recommended order: `Pricing & distribution`, `Content rating`, `Store listing` and `App releases`

    > You can find the required assets for `Store listing` in the `publishing/android` folder


    ![](https://i.stack.imgur.com/C7vDL.png)

- Initialize fastlane
  ```bash
  cd <PROJECT_NAME>/android
  fastlane init
  ```
- Use the Fastfile from `publishing`
  ```bash
  cp publishing/android/fastlane/Fastfile android/fastlane
  ```

- Distribute your app
  ```bash
  fastlane beta
  ```

    >  There is no official plugin to automatically upgrade android version code (unlike the iOS lane).
Before each deployment, be sure to manually upgrade the `versionCode` value inside `android/app/build.gradle`.

#### More
- Checkout the [Fastlane's beta distribution guide](https://github.com/thecodingmachine/react-native-boilerplate/blob/master/docs/beta%20builds.md) for more details
- [Fastlane's documentation](https://docs.fastlane.tools/getting-started/cross-platform/react-native/) for React Native

### Apple Store Connect's missing compliance
If you dont' use Fastlane and you don't want to *Provide Export Compliance Information* at **every push** , then add this to your `Info.plist`
```plist
<key>ITSAppUsesNonExemptEncryption</key>
<false/>
```
![](https://i.stack.imgur.com/i7ret.png)
Note that you might have to set that to `<true/>` if your [app uses encryption](https://developer.apple.com/documentation/bundleresources/information_property_list/itsappusesnonexemptencryption)