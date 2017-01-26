# react-native-file-picker
A React Native module that uses native UI to select a file from the device library.

Project heavily based on [react-native-image-picker](https://github.com/marcshilling/react-native-image-picker).

### note 26/1/2017

This repository is **heavily outdated and** I've been using it with **react native 0.24**, so it propably won't work with newer versions. Try using one of forks, most recent being [this one](https://github.com/luisfuertes/react-native-file-picker).

# Installation

## iOS
not supported

## Android
1. `npm install https://github.com/Lichwa/react-native-file-picker --save`

2. add to `android/settings.gradle`

    ```gradle
    ...

    include ':react-native-file-picker'
    project(':react-native-file-picker').projectDir = new File(settingsDir, '../node_modules/react-native-file-picker/android')
    ```

3. add to `android/app/build.gradle`

    ```gradle
    ...

    dependencies {
        ...
        compile project(':react-native-file-picker')
    }
    ```

4. make sure you have all needed permissions in `android/app/src/main/AndroidManifest.xml`

    ```xml
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
        package="com.myApp">

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.CAMERA" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-feature android:name="android.hardware.camera" android:required="true"/>
        <uses-feature android:name="android.hardware.camera.autofocus" />
        ...
    ```

5. add to `android/app/src/main/java/<project namespace>/MainActivity.java`

    ```java
    ...

    import com.filepicker.FilePickerPackage; // import package

    public class MainActivity extends ReactActivity {

       /**
       * A list of packages used by the app. If the app uses additional views
       * or modules besides the default ones, add more packages here.
       */
        @Override
        protected List<ReactPackage> getPackages() {
            return Arrays.<ReactPackage>asList(
                new MainReactPackage(),
                new FilePickerPackage() // Add package
            );
        }
    ...
    }

    ```

# Usage
1. In your React Native javascript code, bring in the native module:

    ```javascript
    var FilePickerManager = require('NativeModules').FilePickerManager;
    ```

2. Displaying file picker:

    ```javascript
    FilePickerManager.showFilePicker((response) => {
        console.log('Response', response);

        if (response.didCancel) {
            console.log('User cancelled file picker');
        }
        else if (response.error) {
            console.log('FilePickerManager Error: ', response.error);
        }
        else {
            this.setState({
                file: response
            });
        }
    });
    ```
