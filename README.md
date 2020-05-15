# react-native-meteor

---

The purpose of this fork is to keep the dependencies up to date and to keep it inline with Meteor.

---

Meteor-like methods for React Native.

## What is it for ?

The purpose of this library is :

* To set up and maintain a ddp connection with a ddp server, freeing the developer from having to do it on their own.
* Be fully compatible with react-native and help react-native developers.
* **To match with [Meteor documentation](http://docs.meteor.com/) used with React.**

## Install

```
npm i --save https://github.com/bradnorman5490/react-native-meteor.git
```

## Example usage

```javascript
import React, { Component } from 'react';
import { View, Text } from 'react-native';
import Meteor, { withTracker, MeteorListView } from 'react-native-meteor';

Meteor.connect('ws://192.168.X.X:3000/websocket'); //do this only once

class App extends Component {
  renderRow(todo) {
    return <Text>{todo.title}</Text>;
  }
  render() {
    const { settings, todosReady } = this.props;

    return (
      <View>
        <Text>{settings.title}</Text>
        {!todosReady && <Text>Not ready</Text>}

        <MeteorListView
          collection="todos"
          selector={{ done: true }}
          options={{ sort: { createdAt: -1 } }}
          renderRow={this.renderRow}
        />
      </View>
    );
  }
}

export default withTracker(params => {
  const handle = Meteor.subscribe('todos');
  Meteor.subscribe('settings');

  return {
    todosReady: handle.ready(),
    settings: Meteor.collection('settings').findOne(),
  };
})(App);
```

## Documentation

* Learn how to getting started from [connecting your components](docs/connect-your-components.md).
* The [API reference](docs/api.md) lists all public APIs.
* Visit the [How To ?](docs/how-to.md) section for further information.

## Want to help ?

Pull Requests and issues reported are welcome! :)
