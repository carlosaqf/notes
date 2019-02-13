# REACT
[Topics](../README.md)

## What is React?
React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called "components".

```Javascript
class ShoppingList extends React.Component{
    render() {
        return (
            <div className="shopping-list">
                <h1>Shopping List for {this.props.name}</h1>
                <ul>
                    <li>Instagram</li>
                    <li>WhatsApp</li>
                    <li>Oculus</li>
                </ul>
            </div>
        );
    }
}

//Example usage: <ShoppingList name="Carlos" />
```

We use components to tell React what we want to see on screen. When our data changes, React will efficiently update and re-render our components.

Here, ShoppingList is a **React component class**, or **React component type**. A component takes in parameters, called `props` and returns a hierarchy of views to display via the `render` method.

`render` method returns a description of what you want to see on the screen. React takes the description and displays the result. 

In particular, `render` returns a **React element**, which is a lightweight description of what to render. Most React developers use a special syntax called "JSX" which makes these structures easier to write.

Each React component is encapsulated and can operate independently; this allows you to build complex UIs from simple components.

> Note: The DOM `<button>` element's `onClick` attribute has a special meaning to React because it is a built-in component. For custom components like Square, the naming is up to you. We could name the Square's `onClick` prop or Board's `handleClick` method differently. In React, however, it is a convention to use `on[Event]` names for proprs which represent events and `handle[Event]` for the methods which handle the events.

## Functional Components

In React, functional components are a simpler way to write components that only contain a `render` method and don't have their own state. Instead of defining a class which extends `React.Component`, we can write a function that takes `props` as an input and returns what should be rendered. Functional components are less tedious to write than classes, and many components can be expressed this way.

## React Components: State and Props

### State
- Each component can store its own local information in its "state"
    - Private and fully controlled by the component
    - Can be passed as props to children
- Only class components can have local state
- State declared within the constructor:
```Javascript
class Menu extends Component {
    constructor(props){
        super(props);

        this.state = {
            selectedDish: null
        }
    }
    ..
}
```
- State should only be modified using `setState()`
```Javascript
onDishSelect(dish){
    this.setState({
        selectedDish: dish
    });
}
```
- Never do the following:
```Javascript
this.state.selectedDish = dish;
```

### Props
- JSX attributes are passed into a component as a single object
    - Available in the component as "props"
    - Can pass in multiple attributes
    - Cannot modify props within the component
- Examples:
```Javascript
<Menu dishes={this.state.dishes} />
```
- Here the dishes are available as props within the Menu Component and can be accessed as `this.props.dishes`
```Javascript
<Dishdetail dish={this.state.dish} comments={this.state.comments} />
```
- Here dish is available as props within the Dishdetail Component and can be accessed as `this.props.dish`, and comments as `this.props.comments`

### Handling Events
- Handling events is similar to the way you handle events on DOM elements:
    - Use camelCase to specify events
    - Pass funtion as the event handler
- Example:
`<Card onClick={() => this.onDishSelect(dish)}>`

### Lifting State Up
- Sometimes several components may share the same data
- Changes to data in one component needs to be reflected to another component
- Best to move the shared state to a common ancestor component

### Lists and Keys
- Lists are handled similar to JavaScript
- Example:
```Javascript
const menu = this.props.dishes.map((dish) => {
    return (
        <div key={dish.id}>
            <h1>(dish.name)</h1>
            <p>(dish.description)</p>
        </div>
    );
});
```
- Keys should be given to elements inside the array
    - This helps to identify which items have changes, are added or removed

## React Components: Lifecycle Methods

### React Component Lifecycle
- React Component goes through the following lifecycle stages:
    - Mounting
    - Updating
    - Unmounting
- Several lifecycle methods available in each stage

### Mounting Lifecycle Methods
- Called when an instance of a component is being created and inserted into the DOM:
    - `constructor()`
    - `getDerivedStateFromProps()`
    - `render()`
    - `componentDidMount()`
- An earlier method now deprecated called `componentWillMount()`

### Updating Lifecycle Methods
- Called when a component is being re-rendered
    - Can be caused by changes to props or state
    - `getDerivedStateFromProps()`
    - `shouldComponentUpdate()`
    - `render()`
    - `getSnapshotBeforeUpdate()`
    - `componentDidUpdate()`
- Two methods that are now deprecated:
    `componentWillReceiveProps()` and `componentWillUpdate()`

### Unmounting Lifecycle Methods
- Is called when the component is being removed from the DOM:
    - `componentWillUnmount()`
- Error Handling: called when there is an error during rendering, in a lifecycle method or in the constructor of any child component
    - `componentDidCatch()`
