---
label: Angular
---

### Create a project with a specific Angular version
```
npx -p @angular/cli@16.2.14 ng new {projectName}
```

### ngTemplate, ngTemplateOutlet and ngTemplateOutletContext

```Example
<ng-container *ngFor="let l of currentLetters" 
  [ngTemplateOutlet]="letterKey"
  [ngTemplateOutletContext]="{ letter: l }">
</ng-container>

<ng-template #letterKey let-letter="letter">
  <div class="letter-key" (click)="onLetterClick(letter)">{{letter}}</div>
</ng-template>
```

### Navigate to relative, preserve any query params
```Example
this.router.navigate(['edit'], {relativeTo: this.route, queryParamsHandling: 'preserve'});
```
Note: Can also use 'merge' if adding new ones.

### Passing query parameters and fragments

E.g. to change URL to `/servers/5/edit?allowEdit=1#loading`

```Using HTML
<a
  [routerLink]="['/servers', 5, 'edit']"
  [queryParams]="{allowEdit: '1'}
  fragment="loading">
  Link name
</a> 
```

```Using JS
import { Router } from '@angular/router';

constructor(private router: Router) { }

fnName(id: number) {
  this.router.navigate(['/servers', id, 'edit'], {queryParams: allowEdit: '1'}, fragment: 'loading');
}

```

### Retrieve params, query parameters and fragments

```
import { ActivatedRoute } from '@angular/router';

constructor(private route: ActivatedRoute) { }

// not reactive, will not change after component is loaded
const params = this.route.snapshot.params['id'];
const query = this.route.snapshot.queryParams;
const fragment = this.route.snapshot.fragment;

// subscribe to changes, no need to destroy
this.route.params.subscribe(
  params: Params) => {
    query = +params['id'];
  }
);
this.route.queryParams.subscribe();
this.route.fragment.subscribe();
```

Note: params is always string. Convert by adding +params['id']

### Setting up nested routes

```Example
const appRoutes: Routes = [
  { path: 'servers', component: ServersComponent, children: [
    { path: ':id', component: ServerComponent },
    { path: ':id/edit', component: EditServerComponent }
  ]}
]

<router-outlet></router-outlet>
```

### Auth guard for protecting paths
Use either `canActivate` to protect whole path, or `canActivateChild` to protect only the child paths.

```Route
const appRoutes: Routes = [
  { path: 'servers', 
    component: ServersComponent,
    canActivate: [AuthGuard],
    canActivateChild: [AuthGuard],
    children: [
    { path: ':id', component: ServerComponent },
    { path: ':id/edit', component: EditServerComponent }
  ]}
]
```

```AuthGuard
canActivate(route: ActivatedRouteSnapshot,
              state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
    return this.authService.isAuthenticated()
      .then(
        (authenticated: boolean) => {
          if (authenticated) {
            return true;
          } else {
            this.router.navigate(['/']);
          }
        }
      );
  }

  canActivateChild(route: ActivatedRouteSnapshot,
                   state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
    return this.canActivate(route, state);
  }
```

### Get static data from router
```Route
const appRoutes: Routes = [
  { path: 'servers', 
    component: ServersComponent,
    data: {
      msg: 'Hello'
    }
  }
]
```

```JS
constructor(private route: ActivatedRoute) { }

this.route.data.subscribe(
  (data: Data) => {
    const test = data['msg'];
  }
);

```