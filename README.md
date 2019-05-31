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




