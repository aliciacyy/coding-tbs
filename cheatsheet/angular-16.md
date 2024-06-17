---
label: Angular v16-18
---

## Signals 

### Creating signal
```
import { signal } from '@angular/core'
counter = signal(0);
actions = signal<string[]>([]);
```

### Updating signal
```
// just takes the new value
counter.set(1);

// takes old value
counter.update((old) => ...);
actions.update((old) => [...old, 'add']);

```

### Reading and updating signals
```
{{ counter() }}
```

### computed
Values that depend on other signal values that are read during derivation.
```
doubleCounter = computed(() => this.counter() * 2);
```

### effect
Run code whenever a signal changes (all signals).
```
effect(() => );
```

## Standalone components

Benefits:
- Remove the notion of NgModules from the developer experience
- Super easy to develop a fully lazy-loaded application, or migrate an existing monolithic application and make it fully lazy-loaded
- Bundle size reduced

### Declaration
```
// component
@Component({
  selector: "app-hello",
  template: ` <div [ngClass]="{ highlight: true }">Hello World!</div> `,
  imports: [NgClass],
  standalone: true,
})
class StandaloneComponent {

}

// pipes
@Pipe({
  name: "capitalise",
  standalone: true,
})
export class CapitalisePipe implements PipeTransform {
  transform(word: string): string {
    return word.toLocaleUpperCase();
  }
}

// directives
@Directive({
  selector: "[example-directive]",
  standalone: true,
})
class ExampleDirective {

}
```

### Import into other components
```
@Component({
  selector: "parent",
  template: `<hello></hello>`,
  imports: [HelloComponent],
})
class ParentComponent {

}
```

### Bootstrapping standalone components
```
import { bootstrapApplication } 
 from "@angular/platform-browser";

bootstrapApplication(StandaloneComponent);
```
Reference: https://blog.angular-university.io/angular-standalone-components/