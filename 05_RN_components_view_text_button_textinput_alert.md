# Lab 05: RN components view, text, button, textinput, alert
## Lab Task 1: Design the game Layout which contains:
* Title of the Game
* User Input Text Area (User will input the number through onscreen buttons)
* Buttons (0-9) for input number

```
import React, { useState } from 'react';
import { View, Text, TextInput, TouchableOpacity, StyleSheet } from 'react-native';

const GameScreen = () => {
  const [inputValue, setInputValue] = useState('');

  const handleButtonPress = (number) => {
    setInputValue(inputValue + number);
  };

  const handleResetPress = () => {
    setInputValue('');
  };

  const isInputEmpty = inputValue.trim() === '';

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Game Title</Text>
      <TextInput
        style={styles.input}
        placeholder="Enter a number"
        value={inputValue}
        onChangeText={setInputValue}
        keyboardType="numeric"
      />
      <View style={styles.buttonContainer}>
        {Array.from({ length: 10 }, (_, index) => (
          <TouchableOpacity
            key={index}
            style={styles.button}
            onPress={() => handleButtonPress(index)}
          >
            <Text style={styles.buttonText}>{index}</Text>
          </TouchableOpacity>
        ))}
        <TouchableOpacity
          style={[styles.button, isInputEmpty && styles.disabledButton]}
          onPress={handleResetPress}
          disabled={isInputEmpty}
        >
          <Text style={styles.buttonText}>Reset</Text>
        </TouchableOpacity>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    backgroundColor: '#fff',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 16,
  },
  input: {
    width: '80%',
    height: 50,
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 8,
    padding: 8,
    marginBottom: 16,
    fontSize: 16,
  },
  buttonContainer: {
    flexDirection: 'row',
    flexWrap: 'wrap',
    justifyContent: 'center',
    alignItems: 'center',
    width: '80%',
  },
  button: {
    width: '30%',
    height: 50,
    margin: 8,
    backgroundColor: '#0080ff',
    borderRadius: 8,
    alignItems: 'center',
    justifyContent: 'center',
  },
  buttonText: {
    color: '#fff',
    fontSize: 18,
    fontWeight: 'bold',
  },
  disabledButton: {
    backgroundColor: '#ccc',
  },
});

export default GameScreen;
```
