---
label: React
---

### Reusable input components
Instead of defining every key for the props (e.g. id={props.input.id}), you can pass it like this:

```
const Input = (props) => {
  return (
  <div className={classes.input}>
		<label htmlFor={props.input.id}>{props.label}</label>
    <input {...props.input}/>
	</div>);

};
```