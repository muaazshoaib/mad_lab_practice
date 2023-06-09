# Lab 06: RN components and Hooks
## Lab Task 1: Design the basic layout of Tic tac toe application using React native. (9 buttons , Player text and their symbols 0 or X).
```
import React, { useState } from 'react';
import { StyleSheet, Text, View, TouchableOpacity } from 'react-native';

export default function App() {
  const [board, setBoard] = useState(Array(9).fill(null));
  const [player, setPlayer] = useState('X');

  const handlePress = (index) => {
    const newBoard = [...board];
    newBoard[index] = player;
    setBoard(newBoard);
    setPlayer(player === 'X' ? 'O' : 'X');
  };

  return (
    <View style={styles.container}>
      <View style={styles.row}>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(0)}>
          <Text style={styles.cellText}>{board[0]}</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(1)}>
          <Text style={styles.cellText}>{board[1]}</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(2)}>
          <Text style={styles.cellText}>{board[2]}</Text>
        </TouchableOpacity>
      </View>
      <View style={styles.row}>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(3)}>
          <Text style={styles.cellText}>{board[3]}</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(4)}>
          <Text style={styles.cellText}>{board[4]}</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(5)}>
          <Text style={styles.cellText}>{board[5]}</Text>
        </TouchableOpacity>
      </View>
      <View style={styles.row}>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(6)}>
          <Text style={styles.cellText}>{board[6]}</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(7)}>
          <Text style={styles.cellText}>{board[7]}</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.cell} onPress={() => handlePress(8)}>
          <Text style={styles.cellText}>{board[8]}</Text>
        </TouchableOpacity>
      </View>
      <View style={styles.playerContainer}>
        <Text style={styles.playerText}>Current player:</Text>
        <Text style={styles.playerSymbol}>{player}</Text>
      </View>
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
  row: {
    flexDirection: 'row',
  },
  cell: {
    borderWidth: 1,
    borderColor: '#ccc',
    width: 100,
    height: 100,
    alignItems: 'center',
    justifyContent: 'center',
  },
  cellText: {
    fontSize: 48,
    fontWeight: 'bold',
  },
  playerContainer: {
    marginTop: 20,
    flexDirection: 'row',
    alignItems: 'center',
  },
  playerText: {
    fontSize: 24,
    marginRight: 10,
  },
  playerSymbol: {
    fontSize: 48,
    fontWeight: 'bold',
  },
});
```
## Lab Task 2: Design and develop a React native application for the following program given below. The student name and marks of 3 subjects should be input by the user. The submit button should be disabled if any of thefield is empty. After submit, it should be added to the listView below. The Reset button should remove all the items from the listView. 
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
  const [name, setName] = useState('');
  const [subject1, setSubject1] = useState('');
  const [subject2, setSubject2] = useState('');
  const [subject3, setSubject3] = useState('');
  const [data, setData] = useState([]);

  const handleNameChange = (value) => {
    setName(value);
  };

  const handleSubject1Change = (value) => {
    setSubject1(value);
  };

  const handleSubject2Change = (value) => {
    setSubject2(value);
  };

  const handleSubject3Change = (value) => {
    setSubject3(value);
  };

  const handleSubmit = () => {
    if (!name || !subject1 || !subject2 || !subject3) {
      return;
    }

    const newData = [...data, { name, subject1, subject2, subject3 }];
    setData(newData);

    setName('');
    setSubject1('');
    setSubject2('');
    setSubject3('');
  };

  const handleReset = () => {
    setData([]);
  };

  const renderListItem = ({ item }) => (
    <View style={styles.listItem}>
      <Text>{item.name}</Text>
      <Text>Subject 1: {item.subject1}</Text>
      <Text>Subject 2: {item.subject2}</Text>
      <Text>Subject 3: {item.subject3}</Text>
    </View>
  );

  return (
    <View style={styles.container}>
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Student Name"
          value={name}
          onChangeText={handleNameChange}
        />
        <TextInput
          style={styles.input}
          placeholder="Subject 1"
          value={subject1}
          onChangeText={handleSubject1Change}
        />
        <TextInput
          style={styles.input}
          placeholder="Subject 2"
          value={subject2}
          onChangeText={handleSubject2Change}
        />
        <TextInput
          style={styles.input}
          placeholder="Subject 3"
          value={subject3}
          onChangeText={handleSubject3Change}
        />
        <View style={{ flexDirection: 'row', padding: 10 }}>
          <TouchableOpacity
            style={[
              styles.button,
              (!name || !subject1 || !subject2 || !subject3) &&
                styles.disabledButton,
            ]}
            onPress={handleSubmit}
            disabled={!name || !subject1 || !subject2 || !subject3}>
            <Text style={styles.buttonText}>Submit</Text>
          </TouchableOpacity>
          <TouchableOpacity style={styles.button} onPress={handleReset}>
            <Text style={styles.buttonText}>Reset</Text>
          </TouchableOpacity>
        </View>
      </View>
      <FlatList
        data={data}
        renderItem={renderListItem}
        keyExtractor={(item, index) => index.toString()}
        style={styles.list}
      />
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
  inputContainer: {
    alignItems: 'center',
    marginBottom: 20,
  },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 5,
    padding: 10,
    width: '80%',
    marginBottom: 20,
  },
  button: {
    backgroundColor: 'blue',
    padding: 10,
    borderRadius: 5,
    marginTop: 10,
    marginBottom: 10,
    marginLeft: 10,
    marginRight: 10,
  },
  buttonText: {
    color: 'white',
    fontWeight: 'bold',
    textAlign: 'center',
  },
});
```
## Activity 1: Make a To-Do List App using React Native components. The application should add, delete and update items from the list using Hooks. Make sure the styling is same as shown in mobile screen.
```
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
