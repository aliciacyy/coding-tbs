---
label: React (Redux)
---

## Redux vs Context

Context disadvantages:

- You can have a very complex setup and managing state with React Context can become quite complex (deeply nested JSX code)
- Performance (not great for high frequency changes)

Redux:

- One store for all your state for your entire application
- Components subscribe to the store but not the other way one
- Use reducer functions for mutating the store data
- Components dispatch actions, which are forwarded to the reducer

## Setting up (Node.js)

```
const redux = require('redux');

const counterReducer = (state = { counter: 0 }, action) => {
	if (action.type === 'increment') {
		return {
			counter: state.counter + 1
		};
	}
  return state;
}
const store = redux.createStore(counterReducer);

const counterSubscriber = () => {
	const latestState = store.getState(); // gives latest snapshot
};

store.subscribe(counterSubscriber);

store.dispatch({ type: 'increment' });

```

## Setting up (React)
`npm install redux react-redux`

Create `src/store/index.js`

```
import { createStore } from 'redux';

const counterReducer = (state = { counter: 0}, action) => {
	// same as above
}
const store = createStore(counterReducer);

export default store;
```

Connect to index.js:
```
import { Provider } from 'react-redux'
import store from './store/index'

root.render(<Provider store = {store}><App/></Provider>);
```

In component:
```
import { useSelector, useDispatch } from 'react-redux'; // select a part of the state

const Counter = () => {
	const dispatch = useDispatch();
	const counter = useSelector(state => state.counter);
	// automatically subscribe and update component when state changes

	const incrementHandler = () => {
		dispatch({ type: 'increment' });
	}
}
```

## Attach payload to actions
```
const incrementHandler = () => {
	dispatch({ type: 'increment', value: 10 });
}

const counterReducer = (state = { counter: 0 }, action) => {
	if (action.type === 'increment') {
		return {
			counter: state.counter + state.value
		};
	}
  return state;
}

```