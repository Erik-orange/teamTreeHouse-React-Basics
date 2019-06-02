# teamTreeHouse-React-Basics

___
### Components
Functional Component Definition:
```jsx
const MyComponent = (props) {
  return (
    // JSX
  );
}

```

Functional Component Definition with Implicit Return:
```jsx
{props.initPlayers.map( () = >
  // JSX
)}

```

Class Component Definition:
```jsx
class MyComponent extends React.Component {
  // constructor() { ... }
  
  render() {
    return (
      // JSX   {this.props.propName}
      // JSX   {this.state.stateName}
    );
  }
}

```
* In `constructor()` we define the initial `state` that the component will render to (mount).

* The `render()` function in a class component is a function of both `props` and `state`.

* If `state` or `props` change, React executes the `render()` method to update what gets displayed to the user.

**Note:**
* React components return React elements.

* Functional Components are also `state`-less functional componets.

* Class Components are also `state`ful componets.

* Use double quotes, `" "`, when writing `props` to mirror HTML attributes.

* Use curly brackets, `{ }`, when setting numeric values in `props`.
```jsx
// Example
score={23}
```

___

### Using `props` requires two steps:
1. Define the `props` in a component's JSX tag (where it is being used).
2. Enable the use of `props` in a component (define the `props` argument in the function component's definition).



### Props & State
`props` pass data from a parent component to a child component.

`props` is an object, the data in `props` is "_Read-Only_".

`state` is a regular JavaScript object with properties that define the pieces of data that change over time. Data in `state` is "_Read/Write_".

For any data that will change we need to use `state`.

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
class MyComponent extends React.Component {
  eventHandlerFunc() {
    this.setState( {
      statePropName: this.state.statePropName + 1
    });
  }
  
  render() {
    return (
      <button onClick={ this.eventHandlerFunc.bind(this) }>CLICK ME</button>
    );
  }
}
```

**2)** Passing arrow functions to the event (e.g. `onClick={}`) in the component (e.g. button)
```jsx
class MyComponent extends React.Component {
  eventHandlerFunc() {
    this.setState( {
      statePropName: this.state.statePropName + 1
    });
  }
  
  render() {
    return (
      // Uses lexical-this binding
      <button onClick={ () => this.eventHandlerFunc() }>CLICK ME</button>
    );
  }
}
```

**3)** Define the event handler function as an arrow function **[PREFERRED METHOD]**
```jsx
class MyComponent extends React.Component {
  eventHandlerFunc() {
    this.setState( {
      statePropName: this.state.statePropName + 1
    });
  }
  
  render() {
    return (
      <button onClick={ this.eventHandlerFunc }>CLICK ME</button>
    );
  }
}
```

### Change state Based On Previous state
When updating `state` based on a previous `state`, do not rely on `this.state.statePropName` to calculate the next `state` because it may not be accurate.

**To Fix This Issue:**
React's `setState()` method can also take a callback function as an argument instead of an object. This callback function can produce `state` based on a previous `state` in a more reliable form.

```jsx
eventHandlerFunc = () => {
  this.setState( prevState => {     // The 'prevState' parameter can be named anything you'd like
    return {
      statePropName: prevState.statePropName + 1
    };
  });
}
```

* The callback function (an arrow function) receives the previous `state` as it's first argument and the `props` (at the time the update is applied as an optional second argument).

* The only thing that changes over time in React is `state`. 
A change in `state` results in changes to the UI.
Changes to the UI result in changes to the data.

### Remove Items From state
To remove items from a `state` we'll initialize a `state` in the `<App />` component, then create and wire up an event handler that removes an item when an event is triggered, such as a click event.

The component responsible for rendering the desired component will own and maintain that component's `state`. In this case, it's the `<App />` component.

That `state` will be then be passed down and available to the component as well as all children of `<App />` component via `props`.

The `<App />` component **must** be a stateful component for all this to work!

To remove items from `state` wrie the removal function inside the parent component, our example `<App />`, and use the `setState()` method to update the `state` based on `prevState` with the `filter()` method.







