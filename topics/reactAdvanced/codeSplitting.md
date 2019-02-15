# Code-Splitting

## Bundling
Most React apps have files "bundled" using tools like *Webpack* or *Browserify*.

**Bundling** is the process of following imported files and merging them into a single file. This bundle can then be included on a webpage to load an entire app at once.

Ex:

App:
```js
// app.js
import { add } from './math.js';
console.log(add(16, 26)); // 42

//math.js
export function add(a, b){
    return a + b;
}
```

Bundle:
```js
function add(a, b){
    return a + b;
}
console.log(add(16,26)); // 42
```

Bundling grows as your app grows. If you include large third-party libraries it may cause your app to take a long time to load.

To avoid the issue of dealing with a large bundle, you can *split* your bundle.

**Code-Splitting** is a feature supported by bundlers like Webpack and Browserify, which can create multiple bundles that can be dynamically loaded at runtime. 

Code-splitting  your app can help you load only the things that are currently needed by the user, thus improving the performance of your app. 

## import( )
The best way to introduce code-splitting is through the `import()` syntax.

Before:
```js
import { add } from './math';
console.log(add(16,26));
```

After:
```js
import("./math").then(math => {
    console.log(math.add(16,26));
});
```

## React.lazy
The `React.lazy` function lets you render a dynamic import as a regular component

Before:
```js
import OtherComponent from './OtherComponent';
function MyComponent(){
    return (
        <div>
            <OtherComponent />
        </div>
    );
}
```

After:
```js
const OtherComponent = React.lazy(() => import('./OtherComponent'));
function myComponent(){
    return (
        <div>
            <OtherComponent />
        </div>
    );
}
```
This will *automatically load* the bundle containing the `OtherComponent` when this component gets rendered.

`React.lazy` takes a function that must call a dynamic `import()`. This must return a `Promise` which resolves to a module with a `default` export containing a React component.

## Suspense

If the module containing the `OtherComponent` is not yet loaded by the time `MyComponent` renders, you must show fallback content while waiting for it to load - such a a loading indicator. This is done using the `Suspense` component.

```js
const OtherComponent = React.lazy(() => import(./OtherComponent));
function myComponent(){
    return (
        <div>
            <Suspense fallback={<div>Loading...</div>}>
                <OtherComponent />
            </Suspense>
        </div>
    );
}
```

## Error boundaries

If the other module fails to load, it will trigger an error, which we can handle using _Error Boundaries_. Once an error boundary is created, you can use it anywhere above your lazy component to display an error state.

```js
import MyErrorBoundary from './MyErrorBoundary';
const OtherComponent = React.lazy(() => import('./OtherComponent'));
const AnotherComponent = React.lazy(() => import('./AnotherComponent'));
const MyComponent = () => (
    <div>
        <MyErrorBoundary>
            <Suspense fallback={<div>Loading...</div>}>
                <section>
                    <OtherComponent />
                    <AnotherComponent />
                </section>
            </Suspense>
        </MyErrorBoundary>
    </div>
);
```

## Route-based code splitting

Routes are a good place to start with introducing code splitting.

Ex (setup route-based code splitting using libraries like React Router):
```js
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import React, { Suspense, lazy } from 'react';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
    <Router>
        <Suspense fallback={<div>Loading...</div>}>
            <Switch>
                <Route exact path="/" component={Home} />
                <Route path="/about" component={About} />
            </Switch>
        </Suspense>
    </Router>
);
```

## Named Exports

`React.lazy` currently only supports default exports.

If the module you want to import uses named exports, you can create an intermediate module that reexports it as the default.

```js
// ManyComponents.js
export const MyComponent = /* ... */;
export const MyUnusedComponent = /* ... */;

// MyComponent.js
export { MyComponent as default } from "./ManyComponents.js";

// MyApp.js
import React, { lazy } from 'react';
const MyComponent = lazy(() => import('./MyComponent.js'));
```

