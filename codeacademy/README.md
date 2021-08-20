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
### TSX rules

Fine in HTML with a slash:   Fine in JSX:
 
  <br />
 
Also fine, without the slash: NOT FINE AT ALL in JSX:
 
  <br>

* no if statememnts in jsx