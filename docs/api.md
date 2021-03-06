---
id: api
title: API ∙ Universal Router
---

# Universal Router API

## `const router = new Router(routes, options)`

Creates an universal router instance which have a single
[`router.resolve()`](#routerresolve-path-context---promiseany) method.
`Router` constructor expects a plain javascript object for the first `routes` argument
with any amount of params where only `path` is required, or array of such objects.
Second `options` argument is optional where you can pass the following:

- `context` - The object with any data which you want to pass to `resolveRoute` function.<br>
  See [Context](#context) section below for details.
- `baseUrl` - The base URL of the app. By default is empty string `''`.<br>
  If all the URLs in your app are relative to some other "base" URL, use this option.
- `resolveRoute` - The function for any custom route handling logic.<br>
  For example you can define this option to work with routes in declarative manner.<br>
  By default the router calls the `action` function of matched route.

```js
import Router from 'universal-router';

const routes = {
  path: '/',                // string, required 
  name: 'home',             // unique string, optional
  parent: null,             // route object or null, automatically filled by the router
  children: [],             // array of route objects or null, optional 
  action(context, params) { // function, optional

    // action method should return anything except `null` or `undefined` to be resolved by router
    // otherwise router will throw `Page not found` error if all matched routes returned nothing
    return '<h1>Home Page</h1>';
  },
  // ...
};

const options = {
  context: { store: {} },
  baseUrl: '/base',
  resolveRoute(context, params) {
    if (typeof context.route.action === 'function') {
      return context.route.action(context, params);
    }
    return null;
  }
};

const router = new Router(routes, options);
```


## `router.resolve({ path, ...context })` ⇒ `Promise<any>`

Traverses the list of routes in the order they are defined until it finds the first route that
matches provided URL path string and whose `action` function returns anything other than `null` or `undefined`.

```js
const router = new Router([
  {
    path: '/one',
    action: () => 'Page One',
  },
  {
    path: '/two',
    action: () => `Page Two`,
  },
]);

router.resolve({ path: '/one' })
  .then(result => console.log(result));
  // => Page One
```

Where `action` is just a regular function that may, or may not, return any arbitrary data
— a string, a React component, anything!


## Nested Routes

Each route may have an optional `children: [ ... ]` property containing the list of child routes:

```js
const router = new Router({
  path: '/admin',
  children: [
    {
      path: '/',                       // www.example.com/admin
      action: () => 'Admin Page',
    },
    {
      path: '/users',
      children: [
        {
          path: '/',                   // www.example.com/admin/users
          action: () => 'User List',
        },
        {
          path: '/:username',          // www.example.com/admin/users/john
          action: () => 'User Profile',
        },
      ],
    },
  ],
});

router.resolve({ path: '/admin/users/john' })
  .then(result => console.log(result));
  // => User Profile
```


## URL Parameters

**Named route parameters** are captured and added to `context.params`.

```js
const router = new Router({
  path: '/hello/:username',
  action: (context) => `Welcome, ${context.params.username}!`,
});

router.resolve({ path: '/hello/john' })
  .then(result => console.log(result));
  // => Welcome, john!
```

Alternatively, captured parameters can be accessed via the second argument to an action method like so:

```js
const router = new Router({
  path: '/hello/:username',
  action: (ctx, { username }) => `Welcome, ${username}!`,
});

router.resolve({ path: '/hello/john' })
  .then(result => console.log(result));
  // => Welcome, john!
```

This functionality is powered by [path-to-regexp](https://github.com/pillarjs/path-to-regexp) npm module
and works the same way as the routing solutions in many popular JavaScript frameworks such as Express and Koa.
Also check out online [router tester](http://forbeslindesay.github.io/express-route-tester/).


## Context

In addition to a URL path string, any arbitrary data can be passed to the `router.resolve()` method,
that becomes available inside `action` functions.

```js
const router = new Router({
  path: '/hello',
  action(context) {
    return `Welcome, ${context.user}!`;
  },
});

router.resolve({ path: '/hello', user: 'admin' })
  .then(result => console.log(result));
  // => Welcome, admin!
```

Router supports `context` option in the `Router` constructor
to support for specify of custom context properties only once.

```js
const context = {
  store: {},
  user: 'admin',
  // ...
};

const router = new Router(route, { context });
```

Router always adds following parameters to the `context` object
before passing it to the `resolveRoute` function:

- `router` - Current router instance.
- `route` - Matched route object.
- `next` - Middleware style function which can continue resolving,
  see [Middlewares](#middlewares) section below for details.
- `url` - URL which was transmitted to `router.resolve()`.
- `baseUrl` - Base URL path relative to the path of the current route.
- `path` - Matched path.
- `params` - Matched path params,
  see [URL Parameters](#url-parameters) section above for details.
- `keys` - An array of keys found in the path,
  see [path-to-regexp](https://github.com/pillarjs/path-to-regexp) documentation for details.


## Async Routes

The router works great with asynchronous functions out of the box!

```js
const router = new Router({
  path: '/hello/:username',
  async action({ params }) {
    const resp = await fetch(`/api/users/${params.username}`);
    const user = await resp.json();
    if (user) return `Welcome, ${user.displayName}!`;
  },
});

router.resolve({ path: '/hello/john' })
  .then(result => console.log(result));
  // => Welcome, John Brown!
```

Use [Babel](http://babeljs.io/) to transpile your code with `async` / `await` to normal JavaScript.
Alternatively, stick to ES6 Promises:

```js
const route = {
  path: '/hello/:username',
  action({ params }) {
    return fetch(`/api/users/${params.username}`)
      .then(resp => resp.json())
      .then(user => user && `Welcome, ${user.displayName}!`);
  },
};
```


## Middlewares

Any route action function may act as a **middleware** by calling `context.next()`.

```js
const router = new Router({
  path: '/',
  async action({ next }) {
    console.log('middleware: start');
    const child = await next();
    console.log('middleware: end');
    return child;
  },
  children: [
    {
      path: '/hello',
      action() {
        console.log('route: return a result');
        return 'Hello, world!';
      },
    },
  ],
});

router.resolve({ path: '/hello' });

// Prints:
//   middleware: start
//   route: return a result
//   middleware: end
```

Remember that `context.next()` iterates only child routes,
use `context.next(true)` to iterate through the all remaining routes. 


## URL Generation

In most web applications it's much simpler to just use a string for hyperlinks.

```js
`<a href="/page">Page</a>`
`<a href="/user/${username}">Profile</a>`
`<a href="/search?q=${query}">Search</a>`
`<a href="/faq#question">Question</a>`
// etc.
```

However for some types of web applications it may be useful to generate URLs dynamically based on route name.
That's why this feature is available as an add-on with simple API `generateUrls(router, options) ⇒ Function`
where returned function is used for generating urls `url(routeName, params) ⇒ String`.

```js
import Router from 'universal-router';
import generateUrls from 'universal-router/generateUrls';

const routes = {
  path: '/',
  name: 'home',
  children: [
    {
      path: '/user/:username',
      name: 'user',
    },
  ],
};

const router = new Router(routes, { baseUrl: '/base' });
const url = generateUrls(router);

url('home');                          // => '/base'
url('user', { username: 'john' });    // => '/base/user/john'
```

Use `pretty` option for prettier encoding of URI path segments.

```js
const prettyUrl = generateUrls(router, { pretty: true });

url('user', { username: ':' });       // => '/base/user/%3A'
prettyUrl('user', { username: ':' }); // => '/base/user/:'
```

This approach also works fine for dynamically added routes at runtime.

```js
routes.children.push({ path: '/world', name: 'hello' });

url('hello');                         // => '/base/world'
```

