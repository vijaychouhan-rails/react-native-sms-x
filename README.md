## react-native-send-sms
***
**SendSMS**

> ##### A react-native component to send SMS messages. It works only for android. This component used android native api to send sms and response a callback to react-native. This react-native component desn't link to the mobile default messenger view. It will programmatically send the message to a phone number which is provided as a parameter and will response a callback with a string indicating message was sent or failure or no service.

*usage*
```js
import SendSMS from 'react-native-send-sms';

SendSMS.send("+959254687254", "Hey.., this is me!\nGood to see you. Have a nice day.", (msg)=>{ alert(msg) });
```
###### *Note:*

###### Minimum android version is ==4.1== and supported ==RN >= v0.29==.
---
#### Installation
    npm install react-native-send-sms --save
---
##### **Android Setup**

1. In your `android/settings.gradle` file, make the following additions:

```
include ':react-native-send-sms'
project(':react-native-send-sms').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-send-sms/android/app')
```

2. In your `android/app/build.gradle` file, add the ':react-native-send-sms' project as a compile-time dependency:

```
...
dependencies {
    ...
    compile project(':react-native-send-sms')
}
```

3. Update the `MainApplication.java` file as follow:

```js
import com.facebook.react.ReactApplication;
...
import com.someone.sendsms.SendSMSPackage; // <--- add here!


public class MainApplication extends Application implements ReactApplication {

  private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
    @Override
    protected boolean getUseDeveloperSupport() {
      return BuildConfig.DEBUG;
    }

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new SendSMSPackage()     // <--- add here!
      );
    }
  };

  @Override
  public ReactNativeHost getReactNativeHost() {
      return mReactNativeHost;
  }
}
```

4. In your `AndroidManifest.xml` file, add a user permission for sending SMS.

```
<uses-permission android:name="android.permission.SEND_SMS" />
```
---
**Example**

```js
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
  ToastAndroid
} from 'react-native';
import SendSMS from 'react-native-send-sms';

export default class RNSMS extends Component {
  sendSMSFunction() {
    SendSMS.send("+95912345678", "Hey.., this is me!\nGood to see you. Have a nice day.",
      (msg)=>{
        ToastAndroid.show(msg, ToastAndroid.SHORT);
      }
    );
  }
  render() {
    return (
      <View style={styles.container}>        
        <TouchableOpacity style={styles.button} onPress={this.sendSMSFunction.bind(this)}>
          <Text>Send SMS</Text>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },  
  button: {
    padding: 10,
    borderWidth: .5,
    borderColor: '#bbb',
    margin: 10,
    alignItems: 'center',
    justifyContent: 'center'
  }
});

AppRegistry.registerComponent('RNSMS', () => RNSMS);
```