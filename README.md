# Discount Calculator App
```
// Lab 07: useEffect, Image and FlatList
// Lab Task 1: Discount Calculator App

import React, { useState } from 'react';
import {
  StyleSheet,
  Text,
  TextInput,
  TouchableOpacity,
  View,
  Modal,
  FlatList,
} from 'react-native';

export default function App() {
  const [originalPrice, setOriginalPrice] = useState('');
  const [discountPercentage, setDiscountPercentage] = useState('');
  const [discountedPrice, setDiscountedPrice] = useState('');
  const [history, setHistory] = useState([]);
  const [modalVisible, setModalVisible] = useState(false);

  const calculateDiscount = () => {
    if (!originalPrice || !discountPercentage) {
      alert('Please enter both original price and discount percentage');
      return;
    }
    const original = parseFloat(originalPrice);
    const discount = parseFloat(discountPercentage);
    if (
      isNaN(original) ||
      isNaN(discount) ||
      original < 0 ||
      discount < 0 ||
      discount > 100
    ) {
      alert(
        'Please enter valid input. Original price and discount percentage should be positive numbers and discount should be less than 100'
      );
      return;
    }
    const discountAmount = (discount / 100) * original;
    const finalPrice = original - discountAmount;
    setDiscountedPrice(finalPrice.toFixed(2));
    const calculation = `${original} - ${discount}% = ${finalPrice.toFixed(2)}`;
    setHistory([...history, calculation]);
  };

  const clearInputs = () => {
    setOriginalPrice('');
    setDiscountPercentage('');
    setDiscountedPrice('');
  };

  const clearHistory = () => {
    setHistory([]);
  };

  const renderItem = ({ item }) => (
    <Text style={styles.historyItem}>{item}</Text>
  );

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Discount Calculator</Text>
      <TextInput
        style={styles.input}
        placeholder="Enter original price"
        onChangeText={setOriginalPrice}
        value={originalPrice}
        keyboardType="numeric"
        maxLength={10}
      />
      <TextInput
        style={styles.input}
        placeholder="Enter discount percentage"
        onChangeText={setDiscountPercentage}
        value={discountPercentage}
        keyboardType="numeric"
        maxLength={3}
      />

      <TouchableOpacity style={styles.button} onPress={calculateDiscount}>
        <Text style={styles.buttonText}>Calculate Discount</Text>
      </TouchableOpacity>
      {discountedPrice ? (
        <>
          <Text style={styles.result}>
            Discounted Price: ${discountedPrice}
          </Text>
          <TouchableOpacity style={styles.button} onPress={clearInputs}>
            <Text style={styles.buttonText}>Clear Inputs</Text>
          </TouchableOpacity>
        </>
      ) : null}

      {history.length > 0 ? (
        <>
          <TouchableOpacity
            style={styles.button}
            onPress={() => setModalVisible(true)}>
            <Text style={styles.buttonText}>View History</Text>
          </TouchableOpacity>
          <Modal animationType="slide" visible={modalVisible}>
            <View style={styles.modalContainer}>
              <Text style={styles.modalTitle}>Calculation History</Text>
              <FlatList
                data={history}
                renderItem={renderItem}
                keyExtractor={(item, index) => index.toString()}
                style={styles.historyList}
              />
              <TouchableOpacity
                style={styles.button}
                onPress={() => setModalVisible(false)}>
                <Text style={styles.buttonText}>Close</Text>
              </TouchableOpacity>
              <TouchableOpacity style={styles.button} onPress={clearHistory}>
                <Text style={styles.buttonText}>Clear History</Text>
              </TouchableOpacity>
            </View>
          </Modal>
        </>
      ) : null}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
  },
  input: {
    width: '80%',
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    borderRadius: 5,
    marginBottom: 20,
    paddingHorizontal: 10,
  },
  button: {
    backgroundColor: 'blue',
    padding: 10,
    borderRadius: 5,
    marginBottom: 20,
  },
  buttonText: {
    color: 'white',
    fontWeight: 'bold',
    textAlign: 'center',
  },
  result: {
    fontSize: 18,
    fontWeight: 'bold',
  },
});

```

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

# Lab 06: RN components and Hooks
```
// Lab 06: RN components and Hooks

// Activity 1: Make a To-Do List App using React Native components. The application should add, delete and update items from the list using Hooks. Make sure the styling is same as shown in mobile screen.

import React, { useState } from 'react';
import {
  TouchableOpacity,
  ScrollView,
  Button,
  TextInput,
  Text,
  View,
  StyleSheet,
  Keyboard,
} from 'react-native';

export default function App() {
  const [item, setItem] = useState('');
  const [getlist, setList] = useState([]);
  const [editItem, setEditItem] = useState(0);
  const updateList = () => {
    setList((list) =>
      getlist.map((element) =>
        element.key === editItem ? { key: element.key, data: item } : element
      )
    );
    setItem('');
    setEditItem(0);
  };
  const updateItems = (item) => {
    setItem(item.data);
    setEditItem(item.key);
  };
  const additems = () => {
    setList([...getlist, { key: Math.random().toString(), data: item }]);
    setItem('');
    Keyboard.dismiss();
  };
  const deleteItem = (key) => {
    setList((list) => getlist.filter((element) => element.key != key));
  };

  return (
    <View style={{ alignItems: 'center' }}>
      <Text style={{ fontSize: 40 }}>To Do List</Text>
      <TextInput
        style={{ borderBottomWidth: 1, padding: 10, margin: 10 }}
        placeholder=" Enter Text Here "
        value={item}
        onChangeText={setItem}></TextInput>
      <View style={{ flexDirection: 'row' }}>
        <View style={{ marginRight: 10 }}>
          <Button
            title={editItem === 0 ? 'Add item' : 'Update item'}
            onPress={editItem === 0 ? additems : updateList}
            disabled={item.length <= 0}></Button>
        </View>
      </View>
      <Text> {item}</Text>
      <ScrollView style={{ width: '100%' }}>
        {getlist.map((item, index) => (
          <TouchableOpacity
            key={item.key}
            activeOpacity={0.5}
            onPress={() => updateItems(item)}>
            <View
              style={{
                flexDirection: 'row',
                width: '80%',
                alignSelf: 'center',
                backgroundColor: 'red',
                margin: 10,
                borderRadius: 50,
                justifyContent: 'space-between',
              }}
              key={item.key}>
              <Text style={{ fontSize: 20, margin: 10, color: 'white' }}>
                {index + 1}# {item.data} {item.key}
              </Text>
              <TouchableOpacity onPress={() => deleteItem(item.key)}>
                <View
                  style={{
                    backgroundColor: 'black',
                    borderRadius: 50,
                    padding: 5,
                    justifyContent: 'center',
                  }}>
                  <Text
                    style={{
                      fontSize: 20,
                      margin: 5,
                      color: 'white',
                      fontWeight: 'bold',
                    }}>
                    X
                  </Text>
                </View>
              </TouchableOpacity>
            </View>
          </TouchableOpacity>
        ))}
      </ScrollView>
    </View>
  );
}
const styles = StyleSheet.create({});
```

# Lab 05: RN components view, text, button, textinput, alert
```
// Lab 05: RN components view, text, button, textinput, alert

// Activity 1: Make a basic counter application in react native cli, Expo cli and Snack environment.

import { StatusBar } from 'expo-status-bar';
import React, { useState } from 'react';
import { Button, StyleSheet, Text, View } from 'react-native';

export default function App() {
  const [getCount, setCount] = useState(0);
  return (
    <View style={styles.container}>
      <Text style={{ fontSize: 18, fontWeight: 'bold' }}>
        Counter Application
      </Text>
      <View style={styles.just} flexDirection="row">
        <Button
          title="Decrease"
          color="red"
          onPress={() => {
            setCount(getCount - 1);
          }}
          disabled={getCount == 0}></Button>
        <Text> {getCount} </Text>
        <Button
          title="Increase"
          color="green"
          onPress={() => {
            setCount(getCount + 1);
          }}></Button>
      </View>
      <StatusBar style="auto" />
    </View>
  );
}
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  just: {
    padding: 10,
    justifyContent: 'space-evenly',
  },
});
```
