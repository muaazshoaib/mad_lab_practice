# Lab 07: useEffect, Image and FlatList
## Lab Task 1: Discount Calculator App
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
        'Please enter valid input. 
         Original price and discount percentage should be positive numbers and 
         discount should be less than 100'
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
## Lab Task 2: Design and develop the below application for maintaining the student records. The screens shows the addition, searching and deletion of any student record.
```
import React, { useState } from 'react';
import {
  StyleSheet,
  Text,
  View,
  TextInput,
  TouchableOpacity,
  FlatList,
} from 'react-native';

export default function App() {
  const [students, setStudents] = useState([]);
  const [name, setName] = useState('');
  const [gpa, setGpa] = useState('');
  const [semester, setSemester] = useState('');

  const addStudent = () => {
    if (name && gpa) {
      setStudents([
        ...students,
        { id: Math.random(), name: name, gpa: gpa, semester: semester },
      ]);
      setName('');
      setGpa('');
      setSemester('');
    }
  };

  const searchStudent = () => {
    if (name) {
      const filteredStudents = students.filter((student) =>
        student.name.toLowerCase().includes(name.toLowerCase())
      );
      setStudents(filteredStudents);
      setName('');
      setGpa('');
    }
  };

  const sortStudents = () => {
    const sortedStudents = [...students].sort((a, b) => b.gpa - a.gpa);
    setStudents(sortedStudents);
  };

  const handleDelete = (item) => {
    setStudents((list) => list.filter((x) => x.id !== item.id));
  };

  const renderItem = ({ item }) => (
    <View style={styles.item}>
      <Text style={styles.name}>{item.name}</Text>
      <Text style={styles.gpa}>{item.semester}</Text>
      <Text style={styles.gpa}>{item.gpa}</Text>
      <TouchableOpacity onPress={() => handleDelete(item)}>
        {' '}
        <Text>x</Text>
      </TouchableOpacity>
    </View>
  );

  return (
    <View style={styles.container}>
      <TextInput
        style={styles.input}
        placeholder="Name"
        value={name}
        onChangeText={setName}
      />
      <TextInput
        style={styles.input}
        placeholder="Class"
        value={semester}
        onChangeText={setSemester}
      />
      <TextInput
        style={styles.input}
        placeholder="CGPA"
        value={gpa}
        onChangeText={setGpa}
        keyboardType="numeric"
      />
      <TouchableOpacity style={styles.button} onPress={addStudent}>
        <Text>Add</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={searchStudent}>
        <Text>Search</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={sortStudents}>
        <Text>Sort</Text>
      </TouchableOpacity>
      <FlatList
        data={students}
        renderItem={renderItem}
        keyExtractor={(item, index) => index.toString()}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#fff',
  },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 4,
    padding: 10,
    marginBottom: 10,
  },
  button: {
    backgroundColor: '#eee',
    padding: 10,
    borderRadius: 4,
    marginBottom: 10,
    alignItems: 'center',
  },
  item: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    backgroundColor: '#eee',
    padding: 10,
    borderRadius: 4,
    marginBottom: 10,
  },
  name: {
    fontWeight: 'bold',
    marginBottom: 5,
  },
  gpa: {
    fontStyle: 'italic',
  },
});
```
## Activity 1: A simple example of useEffect, where a name of a person is changed after a certain condition using Hooks.
```
// Lab 07: useEffect, Image and FlatList

// Activity 1: A simple example of useEffect, 
// where a name of a person is changed after a certain condition using Hooks.

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
## Activity 2: A JSON data is shown in DATA variable below. Use the FlatList component to show the “title” of each item in JSON data.
```
// Lab 07: useEffect, Image and FlatList

// Activity 2: A JSON data is shown in DATA variable below. 
// Use the FlatList component to show the “title” of each item in JSON data.

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
