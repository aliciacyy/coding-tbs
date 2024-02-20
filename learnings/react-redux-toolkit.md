---
label: React (Redux Toolkit)
---

## Install
`npm install @reduxjs/toolkit`

`npm install react-redux`

You can remove redux from packages as it is already included.

Redux-toolkit will update the state in an immutable way.

## createSlice
```
import { createSlice } from '@reduxjs/toolkit';

const initialState = { counter: 0, showCounter: true }

const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment(state) {
      state.counter++;
    },
    // action is the extra data
    increase(state, action) {
      state.counter = state.counter + action.payload;
    },
    toggleCounter(state) {
      state.showCounter = !state.showCounter;
    }
  }
});

const store = createStore(counterSlice.reducer);
```

## configureStore
```
const store = configureStore({
  reducer: counterSlice.reducer
});

// or create map of reducers
const store = configureStore({
  reducer: {
    counter: counterSlice.reducer
  }
});
```

To dispatch actions. We don't access reducer methods but use methods (action creators).
```
export const counterAcjtions = counterSlice.actions.toggleCounter

// in component:
import { counterActions } from '../store/index';
import { useDispatch } from 'react-redux';

const Counter = () => {
  const dispatch = useDispatch();

  const incrementHandler = () => {
    dispatch(counterActions.increment());
  }

  const increaseHandler = () => {
    dispatch(counterActions.increase(5)); // { type: IDENTIFIER, payload: 5 }
  }
}

```
import { Provider } from 'react-redux';

import store from './store/index';

root.render(<Provider store={store}><App /></Provider>)
```
```

## Working with multiple slices
```index.js
const initialAuthState = { isAuthenticated: false }

const authSlice = createSlice({
  name: 'auth',
  initialState: initialAuthState,
  reducers: {
    login(state) {
      state.isAuthenticated = true;
    },
    logout(state) {
      state.isAuthenticated = false;
    }
  }
});

const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
    auth: authSlice.reducer
  }
});

export const authActions = authSlice.actions;
```

```counter.js
const counter = useSelector((state) => state.counter.counter);
```

```App.js
import { useSelector } from 'react-redux';

function App() {
  const isAuth = useSelector(state => state.auth.isAuthenticated);

  return (
    {!isAuth && <Login/>}
    {isAuth && <UserProfile/>}
  )
}
```

```Auth.js
import { useDispatch } from 'react-redux';
import { authActions } from '../store/index';

const Auth = () => {
  const dispatch = useDispatch();

  const loginHandler = (event) => {
    event.preventDefault();
    dispatch(authActions.login());
  }
}

```

## Splitting code
Create a file for each slice

store
|- auth.js
|- counter.js
|- index.js

In the non index.js files, export the reducer only and the actions.
e.g. `export default counterSlice.reducer` and `export const counterAction = counterSlice.actions;`

In index.js:
```
import counterReducer from './counter

const store = configureStore({
  reducer: { counter: counterReducer }
});
```

## Using async
- Your reducer functions must be pure, side-effect free, and synchronous. So your reducer functions should take some input in the case of the Redux reducer, the old state and the action, and then produce some output.
- Put side effects code in the component (useEffect()) OR in our own action creator functions. Cannot use reducers.

### Use useEffect()
```
const cart = useSelector((state) => state.cart);

useEffect(() => {
  const response = await fetch('https://react-http-aaaa.firebaseio.com/cart.json', 
    {
      method: 'PUT',
      body: JSON.stringify(cart)
    }
  );

  if (!response.ok) {
    throw new Error('');
  }

  const responseData = await response.json();
}, [cart]);
```
We face one problem when using useEffect the way we currently do it: It will execute when our app starts.
It's a problem because this will send the initial (i.e. empty) cart to our backend and overwrite any data stored there.

To fix, add a variable outside so it does not change when the component is reloaded:
```
let isInitial = true;

function App() {
  ...
  useEffect(() => {
    ...
    if (isInitial) {
      isInitial = false;
      return;
    }
  })
}
```

### Use action creator thunk
A thunk is a function that delays an action until later.
We could write an action creator as a thunk, which does not immediately return the action object, but which instead, returns another function which eventually returns the action. So that we can run some other code before we then dispatch the actual action object that we did want to create.

```cart-slice.js
export const sendCartData = (cartData) => {
  return async (dispatch) => {
    // perform any side-effects/async stuff 
    dispatch(...);
  };
};
```

```App.js
useEffect(() => {
  ...
  if (isInitial) {
    isInitial = false;
    return;
  }
  dispatch(sendCartData(cart));
})
```

