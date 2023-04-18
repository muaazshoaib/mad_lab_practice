# Lab 07: useEffect, Image and FlatList
```
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

