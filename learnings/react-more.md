---
label: React (More)
---

## API calls
```
async function fetchMoviesHandler() {
    const response = await fetch("https://swapi.dev/api/films/");
    const data = await response.json();
    const transformed = data.results.map((d) => {
      return {
        id: d.episode_id,
        title: d.title,
        openingText: d.opening_crawl,
        releaseDate: d.release_date,
      };
    });
    setMovies(transformed);
  }
```

## Custom hooks
The function name MUST start with `use`

```
import {useState, useEffect} from 'react';
const useCounter = (forwards = true) => {
  const [counter, setCounter] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
        if (forwards) {
            setCounter((prevCounter) => prevCounter + 1);
        } else {
            setCounter((prevCounter) => prevCounter - 1);
        }
      
    }, 1000);

    return () => clearInterval(interval);
  }, [forwards]);

  return counter;  // can return anything
};
export default useCounter;
```

```
import useCounter from '...'

const ForwardCounter () => {
    const counter = useCounter(false);
}
```

## Validation

### On blur
```
const nameInputBlurHandler = (event) => {
    setEnteredNameTouched(true);

    // add validation below...
}

<input
    onBlur={nameInputBlurHandler}
>
```

## Custom input hooks example with form
Create `use-input.js` file under `src>hooks`
```
import { useState } from 'react';

const useInput = (validateValue) => {
    const [enteredValue, setEnteredValue] = useState('');
    const [isTouched, setIsTouched] = useState(false);

    const valueIsValid = validateValue(enteredValue);
    const hasError = !valueIsValid && isTouched;

    const valueChangeHandler = (event) => {
        setEnteredValue(event.target.value);
    }

    const inputBlurHandler = (event) => {
        setIsTouched(true);
    }

    return {
        value: enteredValue, hasError, valueChangeHandler, inputBlurHandler
    };
}
```
```
const { value: enteredName, hasError: nameError, valueChangeHandler: nameChangeHander, inputBlurHandler: nameBlur, } = useInput(value => value.trim() !== '');
```