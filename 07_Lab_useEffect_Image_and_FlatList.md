# Lab 07 useEffect, Image and FlatList
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
