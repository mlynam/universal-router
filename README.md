<a href="https://www.kriasoft.com/universal-router/" target="_blank">
  <img width="64" height="64" align="right" src="https://raw.githubusercontent.com/kriasoft/universal-router/master/docs/assets/img/tour.png" />
</a>

# Universal Router

[![NPM version](http://img.shields.io/npm/v/universal-router.svg?style=flat-square)](https://www.npmjs.com/package/universal-router)
[![NPM downloads](http://img.shields.io/npm/dm/universal-router.svg?style=flat-square)](https://www.npmjs.com/package/universal-router)
[![Build Status](http://img.shields.io/travis/kriasoft/universal-router/master.svg?style=flat-square)](https://travis-ci.org/kriasoft/universal-router)
[![Coverage Status](https://img.shields.io/coveralls/kriasoft/universal-router.svg?style=flat-square)](https://coveralls.io/github/kriasoft/universal-router)
[![Dependency Status](http://img.shields.io/david/kriasoft/universal-router.svg?style=flat-square)](https://david-dm.org/kriasoft/universal-router)
[![Online Chat](http://img.shields.io/badge/chat_room-%23universal--router-blue.svg?style=flat-square)](https://gitter.im/kriasoft/universal-router)

> A simple middleware-style router for
  [isomorphic](http://nerds.airbnb.com/isomorphic-javascript-future-web-apps/) JavaScript web apps

Visit **[Quickstart Guide](http://slides.com/koistya/universal-router)** (slides) &nbsp;|&nbsp;
Join **[#universal-router](https://gitter.im/kriasoft/universal-router)** on Gitter to stay up to date


## Installation

```bash
$ npm install universal-router --save
```


## Usage

```js
import Router from 'universal-router';

const routes = [
  { path: '/one', action: () => '<h1>Page One</h1>' },
  { path: '/two', action: () => '<h1>Page Two</h1>' },
  { path: '*', action: () => '<h1>Not Found</h1>' }
];

const router = new Router(routes);

router.resolve({ path: '/one' }).then(result => {
  document.body.innerHTML = result;
  // renders: <h1>Page One</h1>
});
```


## Documentation

* [Overview](https://github.com/kriasoft/universal-router/blob/master/docs/README.md)
* [Getting Started](https://github.com/kriasoft/universal-router/blob/master/docs/getting-started.md)
* [Universal Router API](https://github.com/kriasoft/universal-router/blob/master/docs/api.md)


## Browser Support

Universal Router supports all popular browsers, including Internet Explorer 9 and above with following polyfills:
- [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [`Object.assign`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

For compatibility with older browsers that don't support ES5 methods you may need to include 
[`Array.isArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)
and [`Object.create`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)
polyfills before any other code.


## Learn ES6

:mortar_board: &nbsp; **[ES6 Training Course](https://es6.io/friend/konstantin)** by Wes Bos<br>
:green_book: &nbsp; **[You Don't Know JS: ES6 & Beyond](http://amzn.to/2bFss85)** by Kyle Simpson (Dec, 2015)<br>


## Sponsors

Does your company use Universal Router in production? Please consider
[sponsoring this project](https://opencollective.com/universal-router#sponsor).
Your help will allow maintainers to dedicate more time and resources to its development and support.

<a href="https://opencollective.com/universal-router/sponsor/0/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/0/avatar.svg" height="64">
</a>
<a href="https://opencollective.com/universal-router/sponsor/1/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/1/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/sponsor/2/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/2/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/sponsor/3/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/3/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/sponsor/4/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/4/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/sponsor/5/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/5/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/sponsor/6/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/6/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/sponsor/7/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/7/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/sponsor/8/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/8/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/sponsor/9/website" target="_blank">
  <img src="https://opencollective.com/universal-router/sponsor/9/avatar.svg">
</a>


## Backers

♥ Universal Router? [Become a backer](https://opencollective.com/universal-router#backer)
to show your support and help us maintain and improve this open source project.
Get your image on our README with a link to your site.

<a href="https://opencollective.com/universal-router/backer/0/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/0/avatar.svg" height="64">
</a>
<a href="https://opencollective.com/universal-router/backer/1/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/1/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/backer/2/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/2/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/backer/3/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/3/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/backer/4/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/4/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/backer/5/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/5/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/backer/6/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/6/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/backer/7/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/7/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/backer/8/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/8/avatar.svg">
</a>
<a href="https://opencollective.com/universal-router/backer/9/website" target="_blank">
  <img src="https://opencollective.com/universal-router/backer/9/avatar.svg">
</a>


## Related Projects

* [React Starter Kit](https://github.com/kriasoft/react-starter-kit) —
  Isomorphic web app boilerplate (Node.js, React, GraphQL, Webpack, CSS Modules)
* [Node.js API Starter Kit](https://github.com/kriasoft/nodejs-api-starter) —
  Boilerplate and tooling for building data APIs with Node.js, GraphQL and Relay
* [ASP.NET Core Starter Kit](https://github.com/kriasoft/aspnet-starter-kit) —
  Cross-platform single-page application boilerplate (ASP.NET Core, React, Redux)
* [Babel Starter Kit](https://github.com/kriasoft/babel-starter-kit) —
  JavaScript library boilerplate (ES2015, Babel, Rollup, Mocha, Chai, Sinon, Rewire)
* [React App SDK](https://github.com/kriasoft/react-app) —
  Create React apps with just a single dev dependency and zero configuration
* [React Static Boilerplate](https://github.com/koistya/react-static-boilerplate) —
  Single-page application (SPA) starter kit (React, Redux, Webpack, Firebase)
* [History](https://github.com/mjackson/history) —
  HTML5 History API wrapper library that handle navigation in single-page apps


## Support

* [#universal-router](https://gitter.im/kriasoft/universal-router) on Gitter —
  Watch announcements, share ideas and feedback
* [GitHub Issues](https://github.com/kriasoft/universal-router/issues) —
  Check open issues, send feature requests
* [@koistya](https://twitter.com/koistya) on [Codementor](https://www.codementor.io/koistya),
  [HackHands](https://hackhands.com/koistya/)
  or [Skype](https://hatscripts.com/addskype?koistya) — Private consulting


## Contributing

Anyone and everyone is welcome to
[contribute](https://github.com/kriasoft/universal-router/blob/master/CONTRIBUTING.md) to this project.
The best way to start is by checking our [open issues](https://github.com/kriasoft/universal-router/issues),
[submit a new issues](https://github.com/kriasoft/universal-router/issues/new?labels=bug) or
[feature request](https://github.com/kriasoft/universal-router/issues/new?labels=enhancement),
participate in discussions, upvote or downvote the issues you like or dislike, send [pull
requests](https://github.com/kriasoft/universal-router/blob/master/CONTRIBUTING.md#pull-requests).


## License

Copyright © 2015-present Kriasoft, LLC.
This source code is licensed under the MIT license found in the
[LICENSE.txt](https://github.com/kriasoft/universal-router/blob/master/LICENSE.txt) file.
The documentation to the project is licensed under the
[CC BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/) license.


---
Made with ♥ by
Konstantin Tarkus ([@koistya](https://twitter.com/koistya), [blog](https://medium.com/@tarkus)),
Vladimir Kutepov ([frenzzy](https://github.com/frenzzy)) and
[contributors](https://github.com/kriasoft/universal-router/graphs/contributors)
