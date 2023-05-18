---
label: React (Basics)
---

## Basics

### Start a React project
`npx create-react-app <project-name>`


### Building a component

- Create `{componentName}`.js
- Remember to add export default `{componentName}`
- Add CSS as external file

```Example
import './Expenses.css';
import ExpenseItem from './ExpenseItem';
import Card from '../ui/Card';

function Expenses(props) {
    return (
        <Card className='expenses'>
            <ExpenseItem title={props.expenses[0].title} amount={props.expenses[0].amount} date={props.expenses[0].date} />
            <ExpenseItem title={props.expenses[1].title} amount={props.expenses[1].amount} date={props.expenses[1].date} />
            <ExpenseItem title={props.expenses[2].title} amount={props.expenses[2].amount} date={props.expenses[2].date} />
            <ExpenseItem title={props.expenses[3].title} amount={props.expenses[3].amount} date={props.expenses[3].date} />
        </Card>
    );

}

export default Expenses;
```

### Output dynamic data
Use `{}` braces in JSX.

```Example
const title = 'hello'

function ExpenseItem(props) {
  return (
    <div>
      <h2>{title}
    </div>
  );
}
```

### Passing data via props (parent to child)
First add the props to constructor, then get from props.
```
function ExpenseItem(props) {
  return (
    <Card className="expense-item">
      <ExpenseDate date={props.date}/>
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">{props.amount}</div>
      </div>
    </Card>
  );
}
```
Then pass props from the parent component.
```
  <ExpenseItem title={props.expenses[0].title} 
  amount={props.expenses[0].amount} 
  date={props.expenses[0].date} />

```

### Event handling
```
<button onClick={clickHandler}>

const clickHandler = () => {
  console.log('clicked!');
}
```

### States
Use states to store data and trigger re-render
```
import { useState } from 'react';
const [enteredTitle, setEnteredTitle] = useState('');

// to use as object
const [userInput, setUserInput] = useState({
  enteredTitle: '',
  enteredAmount: '',
  enteredDate: '',
});

// set value
<input type="text" value={enteredTitle} onChange={titleChangeHandler}></input>

const titleChangeHandler = (event) => {
  setEnteredTitle(event.target.value);
}

// set if using the object way but updating only 1 field
 setUserInput((prevState) => {
    return {...prevState, enteredTitle: event.target.value};
});
```

### Updating states based on older states
```
const [counter, setCounter] = React.useState(0);
    
const increase = () => {
    setCounter((prevState) => prevState + 1);
}

return (
  <div>
    <p id="counter">{counter}</p>
    <button onClick={increase}>Increment</button>
  </div>
);
```

### Passing data via props (parent to child)
- Child component to have a prop
- Parent component listens to prop

```
// child
const ExpenseForm = (props) => {
  ...
  const submitHandler = (event) => {
    event.preventDefault();
    const expenseData = {
        title: enteredTitle,
        amount: enteredAmount,
        date: new Date(enteredDate),
    };
    props.onSaveExpenseData(expenseData);
  }
}

// parent
<ExpenseForm onSaveExpenseData={onSaveExpenseDataHandler}/>
```
### Two way binding (stateful component)
```
Also known as controlled component. The set and return value is in the parent component.

<input type="text" value={enteredTitle} onChange={titleChangeHandler}></input>

```

### Stateless component
Has no state, just there to output some data.

### Dyanmic output
```
{props.expenses.map((p) => (
  <ExpenseItem title={p.title} 
  amount={p.amount} date={p.date} />
))}
```

### Conditional Content
```
let expensesContent = <p>No expenses found</p> ;

if (filterArr.length > 0) {
  expensesContent = filterArr.map((p) => (
      <ExpenseItem 
      key={p.id}
      title={p.title} 
      amount={p.amount} date={p.date} />
    ))
}

return (
  <div>
    <Card className="expenses">
      <ExpensesFilter
        selected={filterYear}
        onFilterChange={filterChangeHandler}
      />
      {expensesContent}
    </Card>
  </div>
);
```

### Adding styles
```
<input style={{
          borderColor: !isValid ? 'red' : 'black',
          background: !isValid ? 'salmon' : 'transparent'
        }} type="text" onChange={goalInputChangeHandler} />
```

### Add CSS classes dynamically
```
<div className={`form-control ${!isValid ? 'invalid' : ''}`}>
  <label>Course Goal</label>
  <input type="text" onChange={goalInputChangeHandler} />
</div>
```

### Styled components
So that the CSS classes are unique to the components.

`npm install --save styled-components`

```
import styled from 'styled-components';

const Button = styled.button`
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;

&:focus {
  outline: none;
}
`;
```

### Using CSS Modules
Need to name css files as `<name>.modules.css`

```
import styles from './Button.module.css';

const Button = props => {
  return (
    <button type={props.type} className={styles.button} onClick={props.onClick}> 
      {props.children}
    </button>
  )
}
```

### Dynamic styles with CSS Modules

```
return (
    <form onSubmit={formSubmitHandler}>
      <div className={`${styles['form-control']} ${!isValid && styles.invalid}`}>
        <label>Course Goal</label>
        <input type="text" onChange={goalInputChangeHandler} />
      </div>
      <Button type="submit">Add Goal</Button>
    </form>
  );
```

### Use React.Fragment to avoid wrapping in div
```
<React.Fragment>
  <AddUser onAddUser={handleAddUser}></AddUser>
  <UsersList users={usersList}></UsersList>
</React.Fragment>
```

or use `<>` and `</>`

### Use portals to render in different places
Set an element with id
`<div id="backdrop-root"></div>`

```
import ReactDOM from "react-dom";

const Backdrop = (props) => {
  return <div className={styles.backdrop} onClick={props.onConfirm}></div>;
};

const ErrorModal = (props) => {
  return (
    <>
      {ReactDOM.createPortal(
        <Backdrop onConfirm={props.onConfirm}></Backdrop>,
        document.getElementById("backdrop-root")
      )}
    </>
  );
};

```

### Using refs
```
import { useRef } from "react";

const nameInputRef = useRef();

<input
  id="username"
  type="text"
  ref={nameInputRef}
/>
```

### useEffect hook
Can be used for avoiding infinite state update loops, for side effects.
```
import React, { useState, useEffect } from 'react';

const [isLoggedIn, setIsLoggedIn] = useState(false);

// first param is the function to run, second param is dependencies that will cause function to run if they are changed. so empty means run once.
useEffect(() => {
  const isUsedLogged =localStorage.getItem('isLoggedIn');

  if (isUsedLogged === '1') {
    setIsLoggedIn(true);
  }
}, [])

If we don't add `[]`, then it reruns for every change.

```
Execute function only when dependencies are changed.
```
  useEffect(() => {
    setFormIsValid(
      enteredEmail.includes('@') && enteredPassword.trim().length > 6
    );
  }, [enteredEmail, enteredPassword]);
```

Clean up function runs before state function runs, but not before the first time it runs.

```
useEffect(() => {
  ...

  // clean up function
  return () => {
    ...
  }
});
```

### useReducer()
Can be used as replacement for useState() if you need "more powerful state management".

`const [state, dispatchFn] = useReducer(reducerFn, initialState, initFn);`

- state: snapshot used in the component re-render/re-evaluation cycle
- dispatchFn: function that can be used to dispatch a new action (i.e. trigger an update of the state)
- reducerFn: (prevState, action) => newState. A function that is triggered automatically once an action is dispatched (via dispatchFn()) - it receives the latest state snapshot and should return the new, updated state.
- initialState: the initial state
- initFn: function to set the initial state program

### Context API - Producer
Add a producer:

Create a file `store/auth-context.js`
```
import React from 'react';

const AuthContext = React.createContext({
    isLoggedIn: false
});

export default AuthContext;
```

Then wrap in the component
```
return (
    <AuthContext.Provider value={{
      isLoggedIn: isLoggedIn
    }}>
      <MainHeader onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    </AuthContext.Provider>
  );
```

### Context API - Consumer
Method 1 - Use AuthContext.Consumer
```
import AuthContext from '../../store/auth-context';

return (
    <AuthContext.Consumer>
      {(ctx) => {
        return (
          <nav className={classes.nav}>
            <ul>
              {ctx.isLoggedIn && (
                <li>
                  <a href="/">Users</a>
                </li>
              )}
              ...
            </ul>
          </nav>
        )
      }}
    </AuthContext.Consumer>
  );
```

Method 2 (RECOMMENDED) - useContext hook
```
import AuthContext from '../../store/auth-context';

const Navigation = (props) => {
  const ctx = useContext(AuthContext);

  return (
    <nav className={classes.nav}>
      <ul>
        {ctx.isLoggedIn && (
          <li>
            <a href="/">Users</a>
          </li>
        )}
        ...
      </ul>
    </nav>
  );
};
```

### Context limitations
React Context is NOT optimised for high frequency changes!

### Rules of Hooks
Only call React Hooks in React Functions
- React Component Functions
- Custom hooks

Only call Reack Hooks at the Top level
-  Don't call them in nested functions
-  Don't call them in any block statements

ALWAYS add everything you refer to inside of useEffect() as a dependency.

---

### Forward Refs
For when you want to expose things from child component so a parent component can use
```
// 1. useRef in parent
const emailRef = useRef();

//2. useImperativeHandle and  React.forwardRef in child
import React, { useRef, useImperativeHandle } from "react";

const Input = React.forwardRef((props, ref) => {
	const inputRef = useRef();

	const activate = () => {
		inputRef.current.focus();
	}

	useImperativeHandle(ref, () => {
		return {
			focus: activate	
		}
	});

  ...
})

// 3. Call from parent
if (!emailIsValid) {
  emailRef.current.focus();
}
```

### Optimization with React.memo
```
export default React.memo(Button);
```

### useCallback
Use Callback is a hook that allows us to store a function across component executions. So it allows us to tell React that we wanna save a function and that this function should not be recreated with every execution.

```
const handler = () => useCallback(() => {
  ...
}, []);
```
This function has no dependecies and therfore will never change.

### useMemo
useMemo basically allows you to memoize, so basically that means to store any kind of data which you want to store

```
const { items } = props;

const list = useMemo(() => {
  return items.sort((a,b) => a- b);
}, [items]);
```

**Reference:** https://www.udemy.com/course/react-the-complete-guide-incl-redux/
