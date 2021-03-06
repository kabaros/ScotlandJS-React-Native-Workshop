# Chapter 8 - Navigation

### What are the navigation options available in React Native?

- [React Navigation](https://reactnavigation.org/) - a JavaScript solution that is a good starting point with Stack and Tab Navigator.
- [React Native Navigation](https://github.com/wix/react-native-navigation) - currently working on v2.
- [Native Navigation](http://airbnb.io/native-navigation/) - native solution, but not production ready yet.
- [NavigatorIOS](https://facebook.github.io/react-native/docs/navigation#navigatorios) - for iOS only.
- [React Router Native](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-native)

We are going to use **[React Navigation](https://reactnavigation.org/)**. Check this [Pitch & Anti-pitch](https://reactnavigation.org/docs/en/pitch.html) page for the pros and cons.  

Here are the [installation instructions](https://reactnavigation.org/docs/en/getting-started.html#installation).

### Basic Stack Navigator

We are going to use [createStackNavigator](https://reactnavigation.org/docs/en/stack-navigator.html).

```js
createStackNavigator(RouteConfigs, StackNavigatorConfig);
```

Here is the basic Root component:
```js
import React from "react";
import { createStackNavigator } from "react-navigation";
import HomeScreen from "./screens/HomeScreen";
import MapScreen from "./screens/MapScreen";
import ListScreen from "./screens/ListScreen";

const Root = createStackNavigator({
  Home: HomeScreen,
  List: ListScreen,
  Map: MapScreen
});

export default Root;
```
Now let's create our HomeScreen
```js
import React from "react";
import { StyleSheet, Text, View, Button } from "react-native";

export default class HomeScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.text}>Home</Text>

        <Button
          title="Go to Map"
          onPress={() => this.props.navigation.navigate("Map")}
        />
        <Button
          title="Go to List"
          onPress={() => this.props.navigation.navigate("List")}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#f8f8f8",
    alignItems: "center",
    justifyContent: "space-around"
  },
  text: {
    fontSize: 26
  }
});

```
In a similar fashion we create two other screens: ListScreen & MapScreen, but this time with a button pointing back to HomeScreen, like this: 

```js
import React from "react";
import { StyleSheet, Text, View, Button } from "react-native";

export default class ListScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text
          style={{
            fontSize: 26
          }}
        >
          List Screen
        </Text>
        <Button
          title="Go Home"
          onPress={() => console.log(this.props.navigation.navigate("Home"))}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#f8f8f8",
    alignItems: "center",
    justifyContent: "space-around"
  }
});
```
What happens if we want to set up a default screen at the startup time? We can use the optional StackNavigatorConfig object:
```js
{
    initialRouteName: 'Home',
}
``` 
Let's check out this [navigation props](https://reactnavigation.org/docs/en/navigation-prop.html):

```js
console.log(this.props)
```
  
Notice that we now have an empty header. What we want is to add route name to the header on List and Map screen, but hide the header on Home screen. 


### Resources

- [Navigating Between Screens](https://facebook.github.io/react-native/docs/navigation) in React Native docs.
- [Routing & Navigation](https://docs.expo.io/versions/v28.0.0/guides/routing-and-navigation) in Expo docs.
