# JSX
```ts
<a href='http://www.example.com'>Welcome to the Web</a>;
 
const title = <h1 id='title'>Introduction to React.js: Part I</h1>; 
```
* jsx expression must have one outermost element


* to render in the dom 
```ts
import React from 'react';
import ReactDOM from 'react-dom';

// Copy code here:
ReactDOM.render(<h1>Hello world</h1>, document.getElementById('app'));
```

* can say
```ts
const myList = (
    <ul>
        <li>Text 1</li>
        <li>Text 2</li>
        <li>Text 3</li>
    </ul>
)

ReactDOM.render(myList, document.getElementById('app'));
```

* react uses virtual DOM
    * only updates elements that have changed, 
    second render doesnt do anything


* to do JS in jsx
```tsx
    <p>
      {Math.PI.toFixed(20) + 3}
    </p>
```

* event listener
```tsx
const kitty = (
	<img 
        onClick={makeDoggy}
		src="https://content.codecademy.com/courses/React/react_photo-kitty.jpg" 
		alt="kitty" />
);

```

* React *ngIf
```tsx
{!judgmental && <li>Nacho Cheez Straight Out The Jar</li>}
```
*`React *ngFor
```tsx
const peopleLis = people.map(person =>
  // expression goes here:
    <li>{person}</li>
);
```
    * you will need keys sometimes
```tsx
const peopleLis = people.map((person, i) =>
  // expression goes here:
    <li key={'person_' + i}>{person}</li>
);
```

* React without JSX
```tsx
const greatestDivEver = React.createElement(
  "div",
  null,
  "i am div"
);
```
* sample component
```tsx
import React from 'react';
import ReactDOM from 'react-dom';
 
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
};
 
ReactDOM.render(
  <MyComponentClass />,
  document.getElementById('app')
);
```

* if you are having issues with this keyword
https://stackoverflow.com/a/64390850/7513181

```tsx

onToggleLoop (e){
  console.log(this) // wont be undefined
}
onClick={(event) => this.onToggleLoop(event)}

* [creating react apps](https://www.codecademy.com/courses/react-101/articles/how-to-create-a-react-app)

```

* render a component ina component
```tsx
class ProfilePage extends   React.Component {
  render() {
    return (
      <Navbar />
    )
  }
}

ReactDOM.render(<ProfilePage />, document.getElementById('app'));
```


* Component tags can be written like this
  * this.props.children is your react ng-content
```tsx
import React from 'react';
import { List } from './List';

class App extends React.Component {
  render() {
    return (
      <div>
        <List type='Living Musician'>
          <li>Sachiko M</li>
          <li>Harvey Sid Fisher</li>
        </List>
        <List type='Living Cat Musician'>
          <li>Nora the Piano Cat</li>
          <li>Nora the Piano Cat</li>
        </List>
      </div>
    );
  }
}


export class List extends React.Component {
  render() {
    let titleText = `Favorite ${this.props.type}`;
    if (this.props.children instanceof Array) { //Living Musicians,Living Cat Musician
    	titleText += 's';
    }
    return (
      <div>
        <h1>{titleText}</h1>
        <ul>{this.props.children}</ul>
      </div>
    );
  }
}
```
* this props
```tsx
import React from 'react';
import ReactDOM from 'react-dom';

class Button extends React.Component {
  render() {
    return (
      <button>
        {this.props.text}
      </button>
    );
  }
}

// defaultProps goes here:
Button.defaultProps = {
    text: 'I am a button'
}


ReactDOM.render(
  <Button text=""/>, 
  document.getElementById('app')
);
```

* this.setState automatically calls render

* when using useState[1], if its an object, use a fn and spread syntax to update the object,array

* use state good example
```tsx
import React, { Component } from "react";
import NewTask from "../Presentational/NewTask";
import TasksList from "../Presentational/TasksList";

export default class AppClass extends Component {
  constructor(props) {
    super(props);
    this.state = {
      newTask: {},
      allTasks: []
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.handleDelete = this.handleDelete.bind(this);
  }

  handleChange({ target }){
    const { name, value } = target;
    this.setState((prevState) => ({
      ...prevState,
      newTask: {
        ...prevState.newTask,
        [name]: value,
        id: Date.now()
      }
    }));
  }

  handleSubmit(event){
    event.preventDefault();
    if (!this.state.newTask.title) return;
    this.setState((prevState) => ({
      allTasks: [prevState.newTask, ...prevState.allTasks],
      newTask: {}
    }));
  }

  handleDelete(taskIdToRemove){
    this.setState((prevState) => ({
      ...prevState,
      allTasks: prevState.allTasks.filter((task) => task.id !== taskIdToRemove)
    }));
  }

  render() {
    return (
      <main>
        <h1>Tasks</h1>
        <NewTask
          newTask={this.state.newTask}
          handleChange={this.handleChange}
          handleSubmit={this.handleSubmit}
        />
        <TasksList
          allTasks={this.state.allTasks}
          handleDelete={this.handleDelete}
        />
      </main>
    );
  }
}

```

* use effect
    * when you have issues pass an empty array to the second argument of useEffect

```tsx
import React, { useState, useEffect } from 'react';

export default function Timer() {
  const [time, setTime] = useState(0);
  const [name, setName] = useState('');
  useEffect(() => {
      const intervalId = setInterval(() => {
          setTime((prevTime) => prevTime + 1);
      },1000)
      return ()=>{
          clearInterval(intervalId);
      }
  },[])

  const handleChange = ({target}) => {
      setName(target.value)
  }

  return (
    <>
      <h1>Time: {time}</h1>
      <input onChange={handleChange} value={name} />
    </>
  );
}




```

* to listen for a change in one item
```tsx
    const [forecastType, setForecastType] = useState('/daily');

    useEffect(() => {
        alert('Requested data from server...');
        get(forecastType).then((response) => {
            setData(response.data);
        });
    },[forecastType]);
```

* inline style tsx
    * write in camelCase
    * [list of styles that dont assumen px](https://reactjs.org/docs/dom-elements.html)
```tsx
const styleMe = <h1 style={{ background: 'lightblue', color: 'darkred' }}>Please style me! I am so bland!</h1>;
```

* If a component class expects a prop, then you can use propTypes for that component class
```tsx
export class MessageDisplayer extends React.Component {
  render() {
    return <h1>{this.props.message}</h1>;
  }
}

// This propTypes object should have
// one property for each expected prop:
MessageDisplayer.propTypes = {
  message: PropTypes.string
};
```


* An __uncontrolled component__ is a component that maintains its own internal state. 

* The important thing here is that the <input /> keeps track of its own text. You can ask it what its text is at any time, and it will be able to tell you like input.value.

* A controlled component, on the other hand, has no memory. If you ask it for information about itself, then it will have to get that information through props
### TSX rules

Fine in HTML with a slash:   Fine in JSX:
 
  <br />
 
Also fine, without the slash: NOT FINE AT ALL in JSX:
 
  <br>

* no if statememnts in jsx

* only call Hooks at the top level
*  only call Hooks from React functions

* A React component should use props to store information that can be changed, but can only be changed by a different component.

* A React component should use state to store information that the component itself can change.

* should have container and presentational component
    * contianer where the logic is
    * presentational what the user sees