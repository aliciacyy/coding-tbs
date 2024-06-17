---
label: rxjs
---

## Observable
A producer of multiple values, "pushing" them to observers (consumers). An observable represents a stream, or source of data that can arrive over time.

Not often used, just for example:
```
const observable = new Observable((subscriber) => {
  subscriber.next(10); // emits data
  subscriber.complete(10); // indicate complete
});
```

## Observer
A consumer of vaulues delivered by an observable.
```
const observer = {
  next: (value) => { console.log(value); }, // get next value
  error: (error) => { console.log(error) }, // catch error
  complete: () => { console.log('completed'); }// completed
}

observable.subscribe(observer);
```
Any time there is error or complete, any other emissions after will be ignored!

## Subject and BehaviourSubject

### Subject
A special type of observable that allows values to be multicasted to many observers.
```
const sub = new Subject();
sub.next(1);
sub.subscribe(x => {
  console.log('Subscriber A', x);
});
```

### BehaviourSubject
Stores the current value. Able to have an initial value.
```
const subject = new BehaviorSubject(123);
subject.subscribe(console.log);
subject.next(456);
```

### When to use Subject and BehaviourSubject
- Use Subject when you have multiple observers and you want updates as they come.
- Use BehaviourSubject when you have multiple observers and you want the latest updates as soon as they subscribe.

## Pipe and operator
Values will now go through pipe first before reaching observer, which contains operators.

```
const observable = new Observable((subscriber) => {
  subscriber.next(data); // emits data
}).pipe(
  map((value) => {
    return value.data;
  }),
  map((value) => {
    return value.filter((v) => v.status === 'active');
  }),
  map((value) => {
    return value.reduce((sum, user) => sum + user.age, 0);  // reduce array into something
  }),
  map((value) => {
    if (value < 18) throw new Error('error'); // to test error
    else return value;
  }),
);
```

## Convert promise to observable
```
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('resolved');
  }, 1000);
})

const obvsPromise = fromPromise(promise);
```
Can also convert observable back to promise by calling to promise on it.

## Operators

### Creation

#### timer 
After given duration, emit numbers in sequence every specified duration.
```
//emit 0 after 1 second then complete, since no second argument is supplied
const source = timer(1000);
//output: 0
const subscribe = source.subscribe(val => console.log(val));
```

#### interval
Emit numbers in sequence based on provided timeframe.
```
//emit value in sequence every 1 second
const source = interval(1000);
//output: 0,1,2,3,4,5....
const subscribe = source.subscribe(val => console.log(val));
```

#### of
Emit variable amount of values in a sequence and then emits a complete notification.
```
//emits values of any type
const source = of({ name: 'Brian' }, [1, 2, 3], function hello() {
  return 'Hello';
});
//output: {name: 'Brian'}, [1,2,3], function hello() { return 'Hello' }
const subscribe = source.subscribe(val => console.log(val));
```

#### from
Turn an array, promise, or iterable into an observable.
```
const arraySource = from([1, 2, 3, 4, 5]);
const subscribe = arraySource.subscribe(val => console.log(val));
```

### Transformation
#### map
Apply projection with each value from source.
```
//emit (1,2,3,4,5)
const source = from([1, 2, 3, 4, 5]);
//add 10 to each value
const example = source.pipe(map(val => val + 10));
```

#### switchMap
Map to observable, complete previous inner observable, emit values.
On each emission the previous inner observable (the result of the function you supplied) is cancelled and the new observable is subscribed.
```
fromEvent(document, 'click')
  .pipe(
    // restart counter on every click
    switchMap(() => interval(1000))
  )
  .subscribe(console.log);
```

### Filtering
#### filter
Emit values that pass the provided condition.
```
const example = source.pipe(filter(num => num % 2 === 0));
```

#### debounceTime
Discard emitted values that take less than the specified time between output

💡 This operator is popular in scenarios such as type-ahead where the rate of user input must be controlled!
```
this.myFormControl.valueChanges.pipe(
  debounceTime(300)
).subscribe(value => {
  // handle the value after 300ms of inactivity
});
```

#### trottleTime
Emit first value then ignore for specified duration
```
/*
  emit the first value, then ignore for 5 seconds. repeat...
*/
const example = source.pipe(throttleTime(5000));
```

#### scan
Reduce over time.
```
const source = of(1, 2, 3);
// basic scan example, sum over time starting with zero
const example = source.pipe(scan((acc, curr) => acc + curr, 0));
```

#### takeUntil
Emit values until provided observable emits.
```
private destroy$ = new Subject<void>();

observable$
  .pipe(takeUntil(this.destroy$))
  .subscribe(data => console.log(data));

ngOnDestroy() {
  this.destroy$.next();
  this.destroy$.complete();
}
```

#### takeWhile
Emit values until provided expression is false.
```
//allow values until value from source is greater than 4, then complete
source$
  .pipe(takeWhile(val => val <= 4))
  // log: 1,2,3,4
  .subscribe(val => console.log(val));
```

#### first/last
Emit the first/last value or first/last to pass provided expression.
```
const example = source.pipe(first());
const example = source.pipe(last());
```

### Combination

#### zip
After all observables emit, emit values as an array. This operator is ideal when you want to combine values from multiple observables in a pairwise fashion.
```
//emit every 1s
const source = interval(1000);
//when one observable completes no more values will be emitted
const example = zip(source, source.pipe(take(2)));
//output: [0,0]...[1,1]
const subscribe = example.subscribe(val => console.log(val));
```

#### forkJoin
When all observables complete, emit the last emitted value from each.

This operator is best used when you have a group of observables and only care about the final emitted value of each.
```
forkJoin(
  // as of RxJS 6.5+ we can use a dictionary of sources
  {
    google: ajax.getJSON('https://api.github.com/users/google'),
    microsoft: ajax.getJSON('https://api.github.com/users/microsoft'),
    users: ajax.getJSON('https://api.github.com/users')
  }
)
  // { google: object, microsoft: object, users: array }
  .subscribe(console.log);
```

### Error handling

#### catch/catchError
Gracefully handle errors in an observable sequence.
```
const source = throwError('This is an error!');
const example = source.pipe(catchError(val => of(`I caught: ${val}`)));
```

#### retry
Retry an observable sequence a specific number of times should an error occur.
```
const example = source.pipe(
  mergeMap(val => {
    //throw error for demonstration
    if (val > 5) {
      return throwError('Error!');
    }
    return of(val);
  }),
  //retry 2 times on error
  retry(2)
);
```

### Utility
#### do/tap
Transparently perform actions or side-effects, such as logging.
```
const source = of(1, 2, 3, 4, 5);
// transparently log values from source with 'tap'
const example = source.pipe(
  tap(val => console.log(`BEFORE MAP: ${val}`)),
  map(val => val + 10),
  tap(val => console.log(`AFTER MAP: ${val}`))
);
```