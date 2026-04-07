# teamTreeHouse ReactJS Basics


## Components

### Functional Component Definition
```jsx
const MyComponent = (props) => {
    // Local methods and component logic

    return (
        // JSX
    );
}
```

#### Inline `prop` Operations w/o Explict `return` Statement
```jsx
{props.initPlayers.map(p =>
    // JSX
)}
```

### Class Component Definition
```jsx
class MyComponent extends React.Component {
    constructor(props) {
        super(props);
        // Initialize state
        this.state = { ... };
    }

    // Lifecycle Methods: Run After Component Mounts
    componentDidMount() {
        // ...
    }
  
    // Event Handler Functions & JS Code
    handleChange(e){
        this.setState({ ... })
    }

    const sum => (a, b) => { ... };
  
    render() {
        // JS Code

        return (
            // JSX & COMPONENTS
            {this.props.propName}
            {this.state.stateName}
        );
    }
}
```

* In `constructor()` we define the initial `state` that the component will `render` or `mount` to the UI.

* The `render()` function in a Class Component is a function of both `props` and `state`.

* If `state` or `props` change, React _executes_ the `render()` method to update what gets displayed to the user.



> \[!NOTE]
* React components return React elements.
* `React` - The ReactJS top-level API.
* `React DOM` - Adds DOM-specific methods.
* `Babel` - A JavaScript compiler that lets us use ES6+ in older browsers.
* Functional Components are also `state`-_less_ functional componets.
* Class Components are also `state`-_ful_ componets.
* Use double quotes, `" "`, when writing `props` to mirror `HTML` attributes.
* React `elements` are _`immutable`_.
* `Create-React-Application` is a development server that uses WebPack to compile `React`, `JSX`, and `ES6`, and auto-prefixes `CSS` files.
* Use curly brackets, `{ }`, when setting numeric values in `props`.
```jsx
score={23}
```


## Props & State

* `props` pass data from a parent component to a child component.
    * `props` is an `Object`, the data in `props` is "_Read-Only_".
* `state` is a regular JavaScript `Object` with `properties` that define the pieces of data that change over time.
    * Data in `state` is "_Read/Write_".


* For any data that will change we need to use `state`.

* The data in `state` is distributed through `props`.

* To access `props` within a Class Component, you use the `this` keyword.
```jsx
{this.props.myPropName}
```
  
* You can also pass "_handler_" `functions`, or any method that's defined on a React component, to other child components.
* This is how you allow child components to interact with their parent components. You pass methods to child components just like any other `props`.


### Default `props`

```jsx
MyComponent.defaultProps = {userName: "John"};
```


### Using `props` Requires Two Steps:
  1. Define the `props` in a component's `JSX` tag (where it is being used).
  2. Enable the use of `props` in a component (define the `props` argument in the function component's definition).


### Type-Checking With `PropTypes`

```jsx
// General Format
ComponentName.propTypes = {propName: PropTypes.propType.isRequired};
```

```jsx
MyComponent.propTypes = {handleClick: PropTypes.func.isRequired};
MyComponent.propTypes = {userName: PropTypes.string.isRequired};
```


## Initialize `state` In A React Component

#### Constructor Syntax
```jsx
class Counter extends React.Component {
    constructor() {
        super()
        this.state = {
            // JavaScript Object
        };
    }

    // ... ...
}
```

#### Class Property Syntax
```jsx
class Counter extends React.Component {
    state = {
        // JavaScript Object
    };

    // ... ... 
}  
```


## Update Component `state`

* Call `setState()` within your component class passing it an `Object` with `key-value` pairs.
* The `keys` are your `state` properties and the `values` are the updated `state` data.

```jsx
this.setState({
    name: "John",
    age: 20
});
```

1. Write an _event handler_ `function` that updates `state` using React's _built-in_ `setState()` method.
2. Give the component (e.g. button) an `onClick()` event that calls the _event handler_ `function` when triggered. This is done _in-line_ using _camelCase_ notation.
3. When the `state` is updated, React executes `render()` and the change will be visible in our UI.

* You pass React events as a `JSX` expression using curly brackets, `{ }`, and the _event handler_ `function` that will get called when the specified event (e.g. `onClick`) is "_triggered_".

* `state` is **<ins>NEVER</ins>** modified directly! 

* The only way React allows you to update a component's `state` is by using it's _built-in_ `setState()` method and this is done inside the _event handler_ `functions`.



## Binding the `thisContext` In React

* When you create a Class Component that extends from `React.Component`, any custom methods you create are not `bound` to the Class Component you just created.
* You must `bind` custom methods so that `this` refers to your newly created Class Component.

* There are several ways to accomplish this task:

#### (1) Calling The `bind()` Method in the `render()` Method
```jsx
class MyComponent extends React.Component {
    eventHandlerFunc() {
        this.setState( {
            statePropName: this.state.statePropName + 1
        });
    }
  
    render() {
        return (
            <button onClick={this.eventHandlerFunc.bind(this)}>CLICK ME</button>
        );
    }
}
```

#### (2) Passing `arrow functions` to the Event (e.g. `onClick={}`) in the Component (e.g. button)
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

#### (3) Bind The _Event Handler_ `function` Inside the `constructor`. **[PREFERRED METHOD]**
```jsx
class MyComponent extends React.Component {
    constructor(props) {
        super(props);
    
        this.eventHandlerFunc = this.eventHandlerFunc.bind(this);
    }
  
    eventHandlerFunc() {
        this.setState( {
            statePropName: this.state.statePropName + 1
        });
    }
  
    render() {
        return (
            <button onClick={this.eventHandlerFunc}> CLICK ME! </button>
        );
    }
}
```


## Change `state` Based On Previous `state`

* When updating `state` based on a previous `state`, **DO NOT** rely on `this.state.statePropName` to calculate the **next** `state` because it may not be accurate.

#### To Fix This Issue:

* React's `setState()` method can also take a `callback function` as an argument instead of an `Object`.
* This `callback function` can produce `state` based on a **previous** `state` in a more reliable form.

```jsx
eventHandlerFunc = () => {
    this.setState( prevState => {     // The 'prevState' parameter can be named anything you'd like
        return {
            statePropName: prevState.statePropName + 1
        };
    });
}
```

* The `callback function` (an arrow function) receives the **previous** `state` as it's first argument, and the `props` (at the time the update is applied) as an optional second argument.

* The **ONLY** thing that changes over time in React is `state`.
    * A change in `state` results in changes to the UI.
    * Changes to the UI result in changes to the data.



## Remove Items From `state`

* To remove items from  `state` we'll initialize the `state` in the `<App />` component, then create and wire up an _event handler_ that removes an item when an event is _triggered_, such as a `click` event.

* The Component responsible for rendering the desired component will own and maintain that Component's `state`.
* In this case, it's the `<App />` Component.
* That `state` will be then be passed down and available to the Component as well as all children of `<App />` Component via `props`.
* The `<App />` Component **MUST** be a `state`-_ful_ Component for all this to work!
* To remove items from `state` write the removal `function` inside the parent component, our example `<App />`, and use the `setState()` method to update the `state` based on `prevState` with the `filter()` method.







