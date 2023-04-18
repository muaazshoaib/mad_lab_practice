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
## Lab Task 2: Design a login screen having following components in given sequence.
* Title of the application as “Login”.
* ‘user name’ and ‘password’ as a TextInput field.
* A ‘submit’ button to check whether entered credential are correct or not
  * Set a check on user name and password
  * If any of the inputText field is empty, then button should be disabled
  * Show alert “Success login”, if the entered username is “cspeople” and password is “computerscience”
  * If any of them is incorrect, show wrong username or password

```
import React, { useState } from 'react';
import {
  View,
  Text,
  TextInput,
  TouchableOpacity,
  Alert,
  StyleSheet,
} from 'react-native';

const LoginScreen = () => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const [isButtonDisabled, setIsButtonDisabled] = useState(true);

  const handleUsernameChange = (text) => {
    setUsername(text);
    setIsButtonDisabled(text.trim() === '' || password.trim() === '');
  };

  const handlePasswordChange = (text) => {
    setPassword(text);
    setIsButtonDisabled(text.trim() === '' || username.trim() === '');
  };

  const handleButtonPress = () => {
    if (username === 'cspeople' && password === 'computerscience') {
      Alert.alert('Success login');
    } else {
      Alert.alert('Wrong username or password');
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Login</Text>
      <TextInput
        style={styles.input}
        placeholder="Enter your user name"
        value={username}
        onChangeText={handleUsernameChange}
      />
      <TextInput
        style={styles.input}
        placeholder="Enter your password"
        value={password}
        onChangeText={handlePasswordChange}
        secureTextEntry
      />
      <TouchableOpacity
        style={[styles.button, isButtonDisabled && styles.disabledButton]}
        onPress={handleButtonPress}
        disabled={isButtonDisabled}>
        <Text style={styles.buttonText}>Submit</Text>
      </TouchableOpacity>
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
  button: {
    width: '80%',
    height: 50,
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

export default LoginScreen;
```
## Activity 1: Make a basic counter application in react native cli, Expo cli and Snack environment.
```
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
