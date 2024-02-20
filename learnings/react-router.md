---
label: React (Router)
---

## Install router
`npm install react-router-dom`

## Adding router

HomePage is a component.
The element tag takes in JSX code.

```app.js
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

const router = createBrowserRouter([
    {path: '/', element: <HomePage />},
    {path: '/products', element: <ProductsPage/ >}
]);

function App() {
    return <RouterProvider router={router}/>;
}

```

## Another way of defining routes
```
import { createBrowserRouter, createRoutersFromElements, Route } from 'react-router-dom';

const routeDefinitions = createRoutersFromElements(
    <Route>
        <Route path="/" element={<HomePage/>}>
        <Route path="/products" element={<ProductsPage/>}>
    </Route>
)

const router = createBrowerRouter(routeDefinitions);
```

## Navigating between pages
Link component prevents the browser default of sending HTTP request and load the appropriate content.
It will also change the URL without sending a new HTTP request.

```
import { Link } from 'react-router-dom';

function HomePage() {
    return (
        <Link to="/products">Click me</Link>
    )
}
```

## Layouts and nested routes
Add an extra route to act as a wrapper

Root.js
```
import { Outlet } from 'react-router-dom';

function RootLayout() {
    return (
        <>
            <Navigation/>
            <Outlet/>
        <>
    )
}
```

App.js
```
const router = createBrowserRouter([
    {
        path: '/',
        element: <RootLayout/ >,
        children: [
            {path: '/', element: <HomePage />},
            {path: '/products', element: <ProductsPage/ >}
        ]
    }
]);
```

## Show error page with errorElement

Error.js
```
function ErrorPage() {
    return (
        <>
            <MainNavigation />
            <main>
                Oops error
            </main>
        <>
    )
}
```

App.js
```
const router = createBrowserRouter([
    {
        path: '/',
        errorElement: <ErrorPage />,
        element: <RootLayout/ >,
        children: [
            {path: '/', element: <HomePage />},
            {path: '/products', element: <ProductsPage/ >}
        ]
    }
]);
```

## Using NavLink
For feedback for navigation.

