# WHAT IS STATE MANAGEMENT ?

A cleaner way to sotre the state of your app ,
Until now , the cleanest thing you can do is use context API.

But there are better solutions that get rid of the problem that context API has ( unnecessary re-renders)

---

# What is Recoil ?

It is a state management library :

STEP 1 : Create a folder name store -> atom -> count.jsx

`count.jsx`

```jsx
import {atom} form 'recoil';
const countAtom = atom ({
 key : "countAtom " , // Unique id: (with respect to other atoms/ selectors : )
    default : 0 , // Default value (aka initial value : )
})
export default countAtom
```

---

# useRecoilState :

This is used in place of useState hook into the code :
How to use this :

`App.jsx` code using Recoil

```jsx
import { useContext, useMemo, useState } from 'react';
import { CountContext } from './context';
import { RecoilRoot, useRecoilState, useRecoilValue, useSetRecoilState } from 'recoil';
import { countAtom, evenSelector } from './store/atoms/count';
import './App.css';
function App() {
	return (
		<div>
			<RecoilRoot>
				<Count />
			</RecoilRoot>
		</div>
	);
}

function Count() {
	console.log('re-render');
	return (
		<div>
			<CountRenderer />
			<Buttons />
		</div>
	);
}

function CountRenderer() {
	const count = useRecoilValue(countAtom);

	return (
		<div>
			<b>{count}</b>
			<EvenCountRenderer />
		</div>
	);
}

function EvenCountRenderer() {
	const isEven = useRecoilValue(evenSelector);

	return <div>{isEven ? 'It is even' : null}</div>;
}

function Buttons() {
	const setCount = useSetRecoilState(countAtom);
	console.log('buttons re-rendererd');

	return (
		<div>
			<button
				onClick={() => {
					setCount((count) => count + 1);
				}}
			>
				Increase
			</button>

			<button
				onClick={() => {
					setCount((count) => count - 1);
				}}
			>
				Decrease
			</button>
		</div>
	);
}

export default App;
```

---

## What is `useRecoilValue` ?

It is used to access and retrive the value from the recoil state,
Since `recoil` gives us three hooks :

Lets compare it with the useState hook and see what's the difference :
`const [count , setCount] = useState(0);`

1. `useRecoilValue()` : Now here `useRecoilValue()` gives you only the `count` part of the above code , means it will only return the varible part of the value :
   SYNTAX <br/>
   `const count  = useRecoilValue(countAtom)`<br/>
2. `useRecoilState()` : It give you both the variable and the setState function :
   SYNTAX :<br/>
   `const [count , setCount] = useRecoilState(counterAtom)`<br/>
3. `useSetRecoilState() ` : Ths hook allows you to write to a recoil state atom without readnig it. It returns a setter function to update the attom's 	value. This hook is useful when you only need to write to the atom and don't want to trigger a re-render when the atom's value changes :<br/>
   SYNTAX :<br/>
   `const setCount = useSetRecoilState(counterAtom)`<br/>
---

# Syntax for using useRecoilValue :

### First Run the following command to install recoil into the application :

` npm install recoil` <br/>
importing the `useRecoilValue` hook<br/>

```jsx
import { useRecoilValue } from 'recoil';
```

# Define a Recoil state atom , Atom hold individula pieces of state :

```jsx
    import { atom } from 'recoil'
    const counterState  = atom ( {
        key : 'counterState ',
        default : 0; /* Default value of the counterState Value : */
     })
```

#### Use the `useRecoilValue() ` hook to access the value stored in the `counterState` atom.

```jsx
const value = useRecoilValue(counterState);
```

---

## Using the retrieved value in the component

```jsx
return <>The counter is {value}</>;
```

---

# In order to use all these

You need to wrap the application into the `<RecoilRoot>`;

```jsx
import { React } from 'react';
import { RecoilRoot } from 'recoil';

function App() {
	// ... logical code :

	return <RecoilRoot>{/* You components here  */}</RecoilRoot>;
}
```

---
