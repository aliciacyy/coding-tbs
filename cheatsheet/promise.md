---
label: promise
---

## fetch
Allows us to hit HTTP endpoint and return response as Promise.
```
const promise = fetch('...');
promise
  .then(res => res.json())
  .then(user => console.log('user: ', user.title))
  .catch(err => console.log('uhoh));
```

## Creating promise
```
const codeblocker = () => {
  return Promise.resolve().then(v => {
    // your async code here
  });
}
```

## async
```
// no need to put async (name) if return is Promise.resolve()
// if use async, can just return fruits[name]

const getFruit = (name) => {
  const fruits = { ... }
  return Promise.resolve(fruits[name]);
}
```

## await
```
const makeSmoothie = async() => {
  const a = await getFruit('apple');
  ...
}
```

## Promise.all
```
const makeSmoothie = async() => {
  try {
    const a = getFruit('apple');
    const a = getFruit('berry');
    const smoothie = await Promise.all([a,b]);
    return smoothie;
  } catch(err) {
    console.log(err);
  }
}
makeSmoothie.then(console.log);
```

## Promise with loops

### Wait for each loop
This will pause each step of the loop until the promise is resolved.
```
const loop = async() => {
  for (const f of fruits) {
    const emoji = await getFruit(f);
    log(emoji);
  }
}

loop();
```

### Run concurrently
```
const smoothie = fruits.map(v => getFruit(v));
const loop = async() => {
  for await (const emoji of smoothie) {
    log(emoji);
  }
}

loop();
```

