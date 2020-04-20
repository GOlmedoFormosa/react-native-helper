## Set up React Native projects

1. First we need to install the tool to start our project globaly
```
npm i create-react-native-app -g
```
2. Then we can create our project writting the following
```
create-react-native-app nameOfMyApp
```
3. Now we can go inside the folder and start our project
```
  cd nameOfMyApp
  yarn start
```

## Configure IOS Simulator for React Native Development
1. Download and install Xcode.
2. Makes sure you have a least version 9.0.
3. Then go to Xcode -> Preferences -> Locations and in Command Line Tools makes sure you have selected the lastest version. 
4. After that we can click Xcode -> Open Developer Tool -> Simulator and start to work.
5. If we want to lunch another device we can click File -> Open Device -> [IOSVERSION] -> [DEVICE]
6. To run our app we just need to run 
```
  yarn run ios
```
or
```
  npm run ios
```

## Configure Android Emulator for React Navite Development
1. Install Android Studio
2. Install Android SDK
3. Configure the ANDROID_HOME environment variable.
4. Open Android Studio, go to avg manager.
5. Create or open the virtual device.
6. In order to check that everything is working, we can run the following command and see the emulators that are running.
```
  abd devices 
```
7. To run our app we need to run 
```
  yarn run android
```
or
```
  npm run android
```

## Set up ESLint
1. Install ESLint
```
  yarn add --dev eslint
```
2. Init ESLint
```
  ./node_modules/.bin/eslint --init
```
3. The previous command will ask a few question and you can choose popular styles guides (I use Airbnb). It will ask you if you are using React and how you want to store your config file (I use JSON).
4. Then inside our package.json I'll add two scripts. The first one will be lint and the other one lint:fix to fix anything.
```
  "lint": "eslint .",
  "lint": "eslint . --fix"

```
5. Now I can run the lint but if we run it we will see a few erros that could be an error or not depending of the custom style that you will follow, nevertheless you can change that configuration in your config file that is called .eslint.json if you had choose a JSON file. The default value is "extends": "airbnb" but we can use other properties to overwrite them. For example we can allow js files instead of just jsx:
```
  {
    "extends": "airbnb",
    "rules": {
      "react/jsx-filename-extension": [
        2,
        {
          "extensions": [".js",".jsx"]
        }
      ]
    }
  }
```
6. Another example could be the fact that we will have an error using "it" because is not defined, but it is defined and is a default configuration for the create-react-app project, so we can expecify an environment because the jest environment adds a few things such as "it" and "expect", so what we can do is say that within our environment -> jest: true, that is going to tell the linter that we are using those global variables. 
```
  {
    "extends": "airbnb",
    "env": {
      "jest": true
    }
    "rules": {
      "react/jsx-filename-extension": [
        2,
        {
          "extensions": [".js",".jsx"]
        }
      ]
    }
  }
```

## Set up Prettier
1. Install Prettier, we add exact in order to keep a version of prettier and don't update it.
```
  yarn add prettier --dev --exact
```
2. The way we use prettier once is installed is running
```
  yarn prettier --write "*.js"
```
3. We can add the previous command in our package.json
```
  "prettier": "prettier --write '*.js'",
```
4. The problem with this is that somethimes prettier can edit the files and cause errors when we run our linter. For the purpose of fixing this we can add another script into our package.json.
```
  "format-code": "yarn run prettier & yarn run lint:fix",
```
5. But here we have a problem, I mean we won't run this code everytime that we change the code, we can forget it, so in anticipation of our mistakes, we can do the following, first install lint-staged and husky, that are things that will allow us to run formating commands wherever we run a commit, I mean this is tied to our git integration and will run any saved file if we don't have our editor configuration set up. 
```
  yarn add lint-staged husky
```
6. Open your package.json again and add the following command in the script property.
```
  "precommit": "lint-staged",
```
7. Above the script property let's add the following
```
  "lint-staged": {
    "*.js": ["yarn run format-code", "git add"]
  },
```

## Automatic code linting & formating in Visual Studio Code
1. Go to extensions and search for "eslint" and should install the one from Dirk Baeumer and reload your editor. Now, if you make a mistake that is in your rules from your eslint config file, you will see a red underline in your code, and if you hand hover it you will see the why of that error. You can also find errors at the bottom left corner and click the (x) you will see all the eslint issues in the console.
2. The other thing is for prettier, you have to search for "prettier" and you need to pick the package that says "Prettier - Code formatter" from Esben Petersen, but the problem with this is that is not that simple to configure like the previous extension.
3. Press "cmd + ," click in user configuration and try to edit the json file with the next rule, so anytime we run prettier, we will run eslint --fix automatically behind escenes.
```
   "prettier.eslintIntegration": true,
```
4. And then something I like to add in the same place (cmd + ,) but for the workspaces is two things to true. 
```
  "editor.formatOnSave": true,
```

## Extensions for Visual Studio Code and React Native development
- React Native Tools - from Microsoft.
- React-Native/React/Redux snippets for es6/es7 - from EQuimper. 

## Organizing your React Native project

## Run App in Production Mode 
1. Open your ios project using xcode.
```
  open ios/nameOfMyApp.xcodeproj
```
2. Then go into edit Schemma. 
3. Once you have "Run" selected change your "Build Configuration" from "Debug" to "Release".
4. Uncheck "Debug executable" and close. 
5. Run the application from xcode. 
6. Once you finish you should por "Debug" for your build configuration and check "Debug executable".
7. Something that you should do for android is open android/app/src/build.gradle and add a keystore.
8. Android is easier, you should only run the following command
```
  react-native run-android --variant=release
```
9. And if you have an error with the release version in Android that is usually solved removing the debug version from the device and running the previous command again.