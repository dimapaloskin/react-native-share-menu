# react-native-share-menu

Adds the application to the share menu of the device, so it can be launched from other apps and receive data from them.

## Installation

* Install the module

```bash
npm i --save react-native-share-menu
```

## Using Android component

* In `android/settings.gradle`

```gradle
...
include ':react-native-share-menu', ':app'
project(':react-native-share-menu').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-share-menu/android')
```

* In `android/app/build.gradle`

```gradle
...
dependencies {
    ...
    compile project(':react-native-share-menu')
}
```

* Register module (in MainActivity.java)

```java
import com.meedan.ShareMenuPackage;  // <--- import
https://raw.githubusercontent.com/meedan/react-native-share-menu/iOS/screenshots/iOS_menu.png
public class MainActivity extends ReactActivity {
  ......
  @Override
  protected List<ReactPackage> getPackages() {
    return Arrays.<ReactPackage>asList(
      new MainReactPackage(),
      new ShareMenuPackage()  // <------ add here     
    );
  }
  ......

}
```

## Using iOS component

In the share extension `loadView()` method, add:

```Objective-c
[ShareMenuModule setShareMenuModule_itemProvider:itemProvider] ;
```

## Example

```javascript
import React, {
  AppRegistry,
  Component,
  Text,
  View
} from 'react-native';
import ShareMenu from 'react-native-share-menu';

class Test extends Component {
  constructor(props) {
    super(props);
    this.state = {
      sharedText: null
    };
  }

  componentWillMount() {
    var that = this;
    ShareMenu.getSharedText((text :string) => {
      if (text && text.length) {
        that.setState({ sharedText: text });
      }
    })
  }

  render() {
    var text = this.state.sharedText;
    return (
      <View>
        <Text>Shared text: {text}</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('Test', () => Test);
```

## How it looks on Android

<img src="https://raw.githubusercontent.com/caiosba/react-native-share-menu/master/screenshots/menu.png" width="47%"> <img src="https://raw.githubusercontent.com/caiosba/react-native-share-menu/master/screenshots/android.png" width="47%">

## How it looks on iOS
<img src="https://raw.githubusercontent.com/meedan/react-native-share-menu/iOS/screenshots/iOS_menu.png" width="47%"> <img src="https://raw.githubusercontent.com/meedan/react-native-share-menu/iOS/screenshots/iOS_view.png" width="47%">
