# teamTreeHouse-React-Basics

___

* React components return React elements.

Function Component:
```jsx
return (
//  JSX
);
```

Class Component:
```jsx
render() {
  return (
  // JSX
  );
}
```

### Using `props` requires two steps:
1. Define the `props` in a component's JSX tag (where it is being used).
2. Enable the use of `props` in a component (define the `props` argument in the function component's definition).

### Components
Function Components **+** `props`

Class Components **+** `state`


### Props & State
`props` is an object. Data in `props` is "_Read-Only_".

`state` is a regular JavaScript object with properties that define the pieces of data that change over time. Data in `state` is "_Read/Write_".

The data in `state` is distributed through `props`.

### Initialize state In A React Component
**Constructor Syntax:**
```jsx
class Counter extends React.Component {
  constructor() {
    super()
    this.state = {
      // JSX
    };
  }
  // ... ...
} 
```

**Class Property Syntax:**
```jsx
class Counter extends React.Component {
  state = {
    // JSX
  };
  // ... ... 
}  
```

### Update A Component's state
1. Write an event handler function that updates `state` using React's built-in `setState()` method.

2. Give the component (e.g. button) an `onClick()` event that calls the event handler function when triggered. This is done in-line using _camelCase_ notation.

3. When the `state` is updated, React executes `render()` and the change will be visible in our UI.

* You pass React events as a JSX expression using curly brackets, `{ }`, and the event handler function that will get called when the specified (e.g. `onClick`) event is triggered.

* `state` is **never** modified directly! The only way React allows you to update a component's state is by using it's built-in `setState()` method. This is done inside the event handler functions.


### Binding the thisContext In React
When you create a class component that extends from `React.Component`, any custom methods you create are not bound to the class component you just created. You must bind custom methods so that `this` refers to your newly created class component.

There are several ways to accomplish this task:

**1)** Calling the `bind()` method in the `render()` method
```jsx
eventHandlerFunc() {
  this.setState( {
    statePropName: this.state.statePropName + 1
  });
}

<button onClick={ this.eventHandlerFunc.bind(this) }>CLICK ME</button>
```

**2)** Passing arrow functions to the event (e.g. `onClick={}`) in the component (e.g. button)
```jsx
eventHandlerFunc() {
  this.setState( {
    statePropName: this.state.statePropName + 1
  });
}

// Uses lexical-this binding
<button onClick={ () => this.eventHandlerFunc() }>CLICK ME</button>
```

**3)** Define the event handler function as an arrow function [PREFERRED METHOD]
```jsx
eventHandlerFunc = () => {
  this.setState( {
    statePropName: this.state.statePropName + 1
  });
}

<button onClick={ this.eventHandlerFunc }>CLICK ME</button>
```












