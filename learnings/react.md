---
label: React
---

## Basics


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

### Passing data via props
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
---

**Reference:** https://www.udemy.com/course/react-the-complete-guide-incl-redux/
