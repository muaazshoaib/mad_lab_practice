# Lab 07: useEffect, Image and FlatList
```
// Lab 07: useEffect, Image and FlatList

// Activity 1: A simple example of useEffect, where a name of a person is changed after a certain condition using Hooks.

import { Text, View, StyleSheet, Button, Alert } from 'react-native';
import React, { useState, useEffect } from 'react';

export default function Example() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('Shreyar');
  useEffect(() => {
    if (count == 5) {
      setName('Zeeshan');
    }
  });
  return (
    <View style={{ margin: 30 }}>
      <Text> {count}</Text>
      <Text> {name} </Text>
      <Button title="Add" onPress={() => setCount(count + 1)}>
        {' '}
      </Button>
    </View>
  );
}
```
```
// Lab 07: useEffect, Image and FlatList

// Activity 2: A JSON data is shown in DATA variable below. Use the FlatList component to show the “title” of each item in JSON data.

import React from 'react';
import {
  SafeAreaView,
  View,
  FlatList,
  StyleSheet,
  Text,
  StatusBar,
} from 'react-native';
const DATA = [
  {
    id: 'bd7acbea-c1b1-46c2-aed5-3ad53abb28ba',
    title: 'First Item',
  },
  {
    id: '3ac68afc-c605-48d3-a4f8-fbd91aa97f63',
    title: 'Second Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Third Item',
  },
];

const Item = ({ title }) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);
const App = () => {
  const renderItem = ({ item }) => <Item title={item.title} />;
  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={DATA}
        renderItem={renderItem}
        keyExtractor={(item) => item.id}
      />
    </SafeAreaView>
  );
};
const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight || 0,
  },
  item: {
    backgroundColor: '#f9c2ff',
    padding: 20,
    marginVertical: 8,
    marginHorizontal: 16,
  },
  title: {
    fontSize: 32,
  },
});
export default App;
```
