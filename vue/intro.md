# The steps and list of plugins that we might need for serverlsess front-end

## Step 1

### Installing the CLI

To install the Vue CLI, run the following command on a Terminal
`npm install -g @vue/cli

### Creating first project

To create a new Vue.js project, run the following command:
`vue create vue-first-app`

### Pick features manually

- [x] Babel
- [x] Router
- [x] Vuex
- [x] CSS Pre-processors
- [x] Linter
- [x] Unit
- [x] E2E
  
- pick a linter/fomrating config: **Prettier**
- Pick additional lint features: **Lint and fix on commit**
- Pick a unit testing solution:  **Jest**
- pick E2E testing solution: **Cypress**
- place config in **package.json**

### start the app

Navigate to the directory of the app and run `npm run serve`

### ESLint and Prettier

The default configuration file includes a set of ESLint plugins. Typically, every plugin contains a defined set of ESLint custom rules to apply to JavaScript files, or any other file extension.

For instance, the `plugin:vue/essential` is the official ESLint plugin for Vue.js. It allows us to check the `<template>`, and `<script>`, of .vue files with ESLint.

The `eslint:recommended` represents the set of recommended ESLint rules to use.

Finally, the `@vue/prettier` plugin is the ESLint plugin for Prettier formatting for Vue Single
File Components(SFC).

ESLint is highly configurable and accommodates the needs of any app. By default, the ESLint parser is compatible with ECMAScript 5 syntax. However, Vue.js components, and objects, are written with Babel. Therefore, it adds the `babel-eslint` as the default parser for this app.


### VS code integration

ESLint and Prettier both run, and report results, on the command line / terminal. Therefore, to let VS Code know about their results, we need to install two more VS Code extensions.

Open VS Code, and locate the Extensions page. Search for both ESLint, and Prettier extensions, and install them.

While inside VS Code, go to Preferences, and then click Settings. Make sure you select the Workspace tab, and click the Open Settings(JSON) button located at the top right side.

Paste the following JSON content:
```json
{
  "eslint.validate": [
    "vue",
    "javascript",
  ],
  "editor.formatOnSave": false,
  "vetur.validation.template": false,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

The Workspace Settings specifies the following:
- Enable ESLint for Vue, and JavaScript code files
- Disable the `editor.formatOnSave` setting
- Disable the vetur validation for the Vue.js `<template>`. In this case, vetur will only validate the `<style>`, and `<script>`.
- Allow ESLint to auto fix any errors on `editor.codeActionsOnSave.` Formatting usually relates to inserting and removing whitespace, while a source code action removes unnecessary imports, unused variables, etc.

### Axios

[Axios](https://github.com/axios/axios) is a Promise-based HTTP Client for the browser, and Node.js. It offers the following features:

1. Makes [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) from the browser.
2. Makes [http](http://nodejs.org/api/http.html) requests from Node.js.
3. Supports the [Promise API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).
4. Intercepts request and response.
5. Transforms request and response data.
6. Cancels requests.
7. Automatic transforms for JSON data.
8. Client side support for protecting against [XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)


#### Install Axios

`npm install axios --save`

#### Importing inside the components

`import axios from 'axios';`


Then, in order to use Axios to communicate with a remote Web API, you use one of the many
functions available on Axios. Typically, you query for remote data inside the `created()` life-cycle hook in Vue.js component:

```js
created() {
   axios.get(`http://jsonplaceholder.typicode.com/posts`)
   .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
   })
   .catch(e => {
      this.errors.push(e)
})
```

That was just an introduction to using Axios in a Vue app. I recommend reading the following article to gain more knowledge about Axios: [“Vue.js REST API Consumption with Axios”](https://alligator.io/vuejs/rest-api-axios/).

### Vue Router

Client-side routing is at the core of Single Page Apps (SPA). With routing, you can navigate to other screens, or pages, without reloading the entire page.

[Vue Router](https://router.vuejs.org/) is the official router for Vue.js. It deeply integrates with Vue.js core to make building SPAs with Vue.js a breeze. The features include:

1. Nested route/view mapping.
2. Modular, component-based router configuration.
3. Route parameters, query, and wildcards.
4. View transition effects powered by Vue.js' transition system.
5. Fine-grained navigation control.
6. Links with automatic active CSS classes.
7. HTML5 history mode or hash mode, with auto-fallback in IE9.
8. Customizable Scroll Behavior.

There are [hundreds of examples](https://github.com/vuejs/vue-router/tree/dev/examples) that you can explore in order to deepen your understanding.

To see how the Vue Router is enabled, and installed, in the app.
Locate the `src\router\index.js` file content:

```js
import Vue from "vue";
import VueRouter from "vue-router";
import Home from "../views/Home.vue";

Vue.use(VueRouter);
const routes = [
   {
      path: "/",
      name: "Home",
      component: Home
   },
   {
      path: "/about",
      name: "About",
      component: () =>
      import(/* webpackChunkName: "about" */ "../views/About.vue")
   }
];
const router = new VueRouter({
   routes
});
export default router;
```

The code installs Vue Router as a Vue Plugin. Then, it defines a set of routes to be used by Vue Router. You should customize, add, and remove routes as per your app. Finally, the code creates a new instance of the `VueRouter` object with the routes defined. The `VueRouter` instance is exported at the end of the file.

Switch back to the `src\main.js` file, and notice the following:

```js
new Vue({
   router,
   ...
}).$mount("#app");
```

To make the Vue app aware of the routes, you need to pass the VueRouter instance to the main Vue object representing your app.

That’s it for configuring and initializing the Vue Router plugin.
To start using it, you will need to be aware of two major components:

- [Router View](https://router.vuejs.org/api/#router-view)
- [Router Link](https://router.vuejs.org/api/#router-link)

The `Router View` component is a placeholder that you add to indicate, to the Vue Router plugin, where to load components to which the user is navigating.

The `Router Link`component is used to link to one of the predefined routes in the app.

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>
```

### Vuex

[Vuex](https://vuex.vuejs.org/) is a state management library for Vue.js. It serves as a single source of truth for any managed state in your app. It stores the state of all the components in your app in a centralized store. Components can communicate with the store to either update the state, or read it.


The ultimate goal of Vuex is to control mutating the state of your app. With Vuex, mutating the state becomes predictable and regulated. This gives way to a conceptual pattern that’s more
popular in SPAs, which is the **one-way-data-flow**.

![one-way-data-flow](https://i.imgur.com/GebcsY8.png)

1. A Vue Component dispatches a Vuex Action.
2. The Action communicates with a remote Web API. It then **commits** the results into a Vuex Mutation. A Vuex Action is not allowed to mutate the state. It does so by means of
a Vuex Mutation.
3. The Mutation mutates the Vuex Store’s State object. The State is shared across all
components in a Vue app.
4. The State is now mutated. Vuex triggers the Vuex Reactive Getters to read fresh data
from the State.
5. The Vue engine detects a change in the value of the Vuex Getters; it renders the new
data, and refreshes the affected components.

Make sure you read the [Vuex documentation](https://vuex.vuejs.org/guide/)

To see how the Vuex is enabled, and installed, in the app locate the `src\store\index.js` file content:

```js
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

export default new Vuex.Store({
   state: {},
   mutations: {},
   actions: {},
   modules: {}
});
```
This code installs Vuex as a Vue Plugin. Then, it creates a new instance of `Vuex.Store` object. The store object contains four main properties:

- **State:** This object holds all the state elements managed by the store.
- **Mutations:** This object holds all the mutation functions available by the store.
- Actions: This object holds all the action functions available by the store.
- **Modules:** This object holds all the different modules created as part of the store. You can layout and structure your store by means of independent modules. That’s an advanced topic, and I suggest consulting with the [Vuex documentation](https://vuex.vuejs.org/guide/modules.html) to learn more about Vuex Modules.

You can go through this basic [Vuex Counter app](https://jsfiddle.net/n9jmu5v7/1269/) to understand how Vuex works.

Switch back to the `src\main.js` file, and notice the following

```js

new Vue({
  …
store,
  ...
}).$mount("#app");

```

To make the Vue app aware of the Vuex store, you need to pass the `Vuex.Store` instance to the main Vue object, representing your app.

### Vue Apollo
“GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. It provides a complete and coherent description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.”

If you are planning to use GraphQL in your Vue app, you should be checking the [Vue Apollo](https://vue-apollo.netlify.com/) Plugin. It integrates [Apollo](https://www.apollographql.com/) into your Vue app.

Apollo is a GraphQL implementation standard for the client-side, and server-side. You can implement GraphQL on the backend/server using [Apollo Server](https://www.apollographql.com/docs/apollo-server/).

On the client-side (React, Vue, or
Angular), you can use [Apollo Client](https://www.apollographql.com/docs/react/) to communicate with the Apollo Server.

To install Vue Apollo, check this detailed guide on how to do so: [Vue Apollo Installation](https://vue-apollo.netlify.com/guide/installation.html#_1-apollo-client).

To start using Vue Apollo in your Vue app, check this detailed guide: [Using Vue Apollo](https://vue-apollo.netlify.com/guide/apollo/#apollo-options).

### Storybook and Component-based development

Developers and designers spend most of their time designing and building the frontend of an app. A common trend is to build small UI components, and then assemble them together inside a Page or View. This brings modularity to the code you write, and allows you to build things faster.

Following this trend, several libraries emerged to help document, and test, components. For instance, [Storybook](https://storybook.js.org/), a library that is used with React.js, Vue.js and Angular frameworks. With Storybook, you build your UI components, and then write Storybook stories to consume those components. Think of it as doing Component Unit Testing.

### Debugging Vue.js apps
We spend a big chunk of our time debugging our code! It’s expected, and part and parcel of the process. In this section, I will share a few debugging methods that I use.

1. [Debugging Vue.js apps inside VS Code](https://vuejs.org/v2/cookbook/debugging-in-vscode.html) explains what you need to
configure your VS Code editor to allow for debugging Vue.js apps.
2. [Debugging Vue.js apps inside Chrome DevTools 101](https://www.youtube.com/watch?v=H0XScE08hy8) explains, in detail, how to use Chrome devtools to debug any JavaScript code, and is not limited to Vue.js only. In addition, you can check the [FireFox DevTools for debugging](https://developer.mozilla.org/en-US/docs/Tools) that details how to use FireFox devtools to debug any JavaScript code, including, but not limited to, Vue.js.
3. [Vue DevTools](https://github.com/vuejs/vue-devtools) is a browser devtools extension for debugging Vue.js applications. This is the best way to inspect your Vue.js components from inside of the browser. You will be able to see what components your view is
composed of, what the internal state of a component is, and view the data properties and computed properties, among other things. Also, if you use the Vuex store in your app, you can view its state by viewing the data, actions, mutations, and getters in the
state.

Finally, watch the [3 Ways to Debug Vue.js apps](https://www.youtube.com/watch?v=lyGt1TmleoU) video. It’s comprehensive, and covers three different ways for debugging. The methods include: VS Code, Chrome devtools, and Vue devtools debugging.
