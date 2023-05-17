---
layout: post
title:  "Basics of React and Redux"
date:   2023-02-02 12:11:31 +0100
categories: React Redux
tags: [React, Redux, JS]
---

These rough notes on React and Redux were made whilst completing A sololearn course, and personal resarch.

## Basics

DOM - document object model

The public folder contains files related to how the application will display on the client, the most important of those being index.html, which is the HTML template of our page:

The src folder contains all of the JavaScript, CSS, and image files that will be compiled into a bundle file and injected into index.html:

Webpack bundles the src code into a single file

Virtual DOM, holds objects values for app, and compares changes from previous state, then applies changes

-   Tree like model

### Rendering JSX

```jsx
ReactDOM.render(

  <h1>Hello, React!</h1>,

  document.getElementById('root')

);

//or 

jsx
const name = "David";
const id= "FNAME";

const el = <p id={id}>Hello, {name}</p>;

ReactDOM.render(

  el,

  document.getElementById('root')

);
```

## Counter / second

```jsx
let counter = 0; // initial value

function show() {

  counter++;

  const el = <p>{counter}</p>;

  ReactDOM.render(

    el, document.getElementById('root')

  );

}

setInterval(show, 1000); // update per second
```

### Counter using state and click events

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import './style.css';

class Counter extends React.Component {
  state = {
    counter: 0,
  };

  increment = () => {
    this.setState({ counter: this.state.counter + 1 });
  };

  render() {
    return (
      <>
        <p>{this.state.counter}</p>
        <button onClick={this.increment}>increment</button>
      </>
    );
  }
}

ReactDOM.render(<Counter />, document.getElementById('root'));
```

### Counter using hooks

```jsx
import React, { useState } from 'react';

function Counter(){
  const [count, setCount] = useState(0)
  function increment(){
    setCount(count + 1)
  }

  return <>
  <p>{count}</p>
  <button onClick={increment}>increment</button>
</>
;

}

ReactDOM.render(<Counter />, document.getElementById('root'));
```

### Counter using redux

```jsx
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import { connect } from 'react-redux';

const initialState={
  count:0
}

function incrementCounterAction(number){
  return{
    type:'INCREMENT',
    num: number
  }
}

function Counter(props){

  function handleClick(){
    props.incrementCounterAction(1);
  }

  return <><p>{props.count}</p>
  <button onClick={handleClick}>Increment</button></>
  
}

function reducer(state=initialState,action){
  switch(action.type){
    case 'INCREMENT':
      return {
        count: state.count+action.num
      }
    default:
      return state;
  }
}

function mapStateToProps(state) {
  return {
    count: state.count
  };
}

const mapDispatchToProps = {
  incrementCounterAction
}

const store = createStore(reducer)

const Counterer = connect(mapStateToProps, mapDispatchToProps)(Counter);

function App() {
  return (
    <Provider store={store}>
      <Counterer/>
    </Provider>
  );
}

export default App;
```

## Functions

```jsx
function Hello() {
  return <h1>Hello world.</h1>;
}
const el = <Hello />; 
ReactDOM.render(
  el, 
  document.getElementById('root')
);
```

## Class components

```jsx
class Hello extends React.Component {
  render() {
    return <h1>Hello world.</h1>;
  }
}

//// using props

class Hello extends React.Component {

  render() {

    return <p>Hello, {this.props.name}!</p>;

  }

}
```

## Props

components cannot modify their props

```jsx
function hello(props){
	return <p> Hello, {props.name}!</p>;
}

// calling fucntion
const el = <hello name="Alan"/>
```

## State

state is used for data where the value can change such as inputs

```jsx
class Hello extends React.Component {

  state = {

    name: "James"

  }

  render() {

    return <h1>Hello {this.state.name}.</h1>;

  }

}
```

States values are updated using setState

-   This will automatically update the render

```jsx
**this.setState**({ 
  name: "James",
  age: 25
});
```

## Hooks

use state in functional components

```jsx
import React, { useState } from 'react';

function Hello() {
  const [name, setName] = useState("David");
  return <h1>Hello {name}.</h1>;
}
```

**useState**

returns a pair, the current state value and a function, that lets you change the state.

**useState**

takes one argument, which is the initial value of the state.

## Lifecycle Methods

Called when components are:

-   mounted, updated or unmounted

**Mounting**

is the process when a component is rendered on the page.

```jsx
componentDidMount() {
  this.setState({counter: 42});
}
```

**Unmounting**

is the process when a component is removed from the page.

### Use effect

run when mounted, updated or unmounted a functional component

have useEffect within the function

mounted

```jsx
import React, { useState, useEffect } from 'react'
useEffect(() => {

    alert("Number of clicks: " + counter);

  });
```

updated value of count

```jsx
import React, { useState, useEffect } from 'react'
useEffect(() => {
  //do something
}, **[count]**);
```

dismounted

```jsx
import React, { useState, useEffect } from 'react'
useEffect(() => {

  // do something

  

  return () => {

    // cleanup

  }; 
});
```

## Events

Button

```jsx
function Counter() {
  const [counter, setCounter] = useState(0);
  function increment() {
    setCounter(counter+1);
  }
  return <div>
  <p>{counter}</p>
  <button **onClick={increment}**>Increment</button>
  </div>;
}
```

Text box

```jsx
function Converter() {
  const [km, setKm] = useState(0);
  function handleChange(e) {
    setKm(e.target.value);
  }
  function convert(km) {
    return (km/1.609).toFixed(2);
  }
  return <div>
  <input type="text" value={km}
     **onChange={handleChange}** />
  <p> {km} km is {convert(km)} miles </p>
  </div>;
}
```

Forms

```jsx
function AddForm() {
  const [sum, setSum] = useState(0);
  const [num, setNum] = useState(0);
  function handleChange(e) {
    setNum(e.target.value);
  }
  function handleSubmit(e) {
    setSum(sum + Number(num));
    e.preventDefault();
  }
  return <form **onSubmit={handleSubmit}**>
  <input type="number" value={num} o**nChange={handleChange}** />
  <input type="submit" value="Add" />
  <p> Sum is {sum} </p>
  </form>;
}
```

## Display each item from list

```jsx
function MyList(props) {
  const arr = props.data;
  const listItems = arr.map((val) =>
    <li>{val}</li>
  );
  return <ul>{listItems}</ul>;
}
```

auto generating keys

```jsx
const listItems = arr.map((val, index) =>
  <li **key={index}**>{val}</li>
);
```

## Redux

Creates a single container of all states which can be assessed by all components

### Store

state should be stored in object called store

There should only be one store object per application

You cannot change a state directly, you have to dispatch an action

```jsx
{
    contacts:{
        name:{"maisie"},
        name:{"john"}
    },
    toggle:true
}
```

-   Single source of truth
-   State is read only
    -   Only changed with actions and reducers
-   Pure reducers
    -   Cannot change state
    -   They modify state and return a new state object with the modifications

### Actions and reducers

Action:
An action is a JSON object

```json
{
	type:'Add_EMPLOYEE',
	name: 'John'
}
```

Actions can be dispatched from anywhere in the app as a ‘payload of information’

Type written in snake case as standard

```json
{
	type:'Add_EMPLOYEE',
	payload:{
		name: 'John'
	}
}
```

Define an action creator to generate payloads
```Javascript
function addEmployee(person){
	return{
		type:'Add_EMPLOYEE',
		payload:person
	}
}
```

Reducer:

input: current state and parameters

returns: new state

it can handle multiple actions at once using a switch statement
```js
function employeeManager(state,action){
	if(action.type == 'Add_EMPLOYEE'){
		return [...state,action.name]
	}
	else{
		return state
	}
}
```
multiple reducers (e.g. invoice, users, products …)

this helps with separation of concerns as you can separate reducers, but only call one

```jsx
const contactsApp = **combineReducers**({
  addContacts,
  doSomething
})
```

## React with redux

installation

```jsx
npm install redux // redux lobary

//then install

npm install react-redux // this binds react with redux allowing componats to read from the reduc store, dispatch actions and update date
```

### Creating store

```jsx
import { Provider } from 'react-redux';
import { createStore } from 'redux';

const store = **createStore(reducer)**;
```

to pass the store down to child component, use provider

```jsx
<Provider store={store}>
    <Counter/>

  </Provider>;
```

### Connecting to store

already: made action, reducer, store and made them available to the component using a provider

```jsx
function connect(mapStateToProps?, mapDispatchToProps?)
```

map to props

```jsx
function mapStateToProps(state) {

  return {

    count: state.count

  };

}
```

-   called every time the store state changes

map dispatch to props

```jsx
const mapDispatchToProps = {
  incrementCounter
}
```

-   returns state variables and functions as props

connect

```jsx
const Counterer = connect(mapStateToProps, mapDispatchToProps)(Counter);
```

## Structure - export files and maintain redux store

-   Separate components
-   you must export functions to use in other components

```jsx
export default connect(mapStateToProps, mapDispatchToProps)(Counter);
```

-   to import in another file

```jsx
import Counter from './Counter';
```

example

[react redux counter example](https://stackblitz.com/edit/react-redux-counter-example-2?file=Counter.js) Made by [sololearninc](https://stackblitz.com/@sololearninc)
