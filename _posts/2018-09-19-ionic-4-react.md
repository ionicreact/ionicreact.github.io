---
layout: post
title: Using React with Ionic v4
subtitle: In this tutorial, you'll learn to use React with Ionic v4
tags:
  - ionic
  - react
published: true
---
Ionic is now framework agnostic which means you can use it with your prefered front-end framework or libray such as React or Vue etc.

As of this writing, the Ionic CLI v4 does only support generating Ionic 4 projects with Angular. In this tutorial, we'll learn how to use React instead of Angular.

## Using React in Your Ionic Application

We can use Ionic CLI v4 to generate an Ionic/Angular v4 application but how about using React?

First, let's start by creating a new project based on Angular:

```bash
ionic start ionic-react-demo blank --type=angular
```

For now we use `--type=angular` but since the Ionic team intends to add React support, in the future we'll probably be able to use `--type=react` to generate an Ionic/React v4 project without the further configurations we'll see next.

## Adding React Libraries

Now, let's add React support to our project by first installing the React core libraries i.e `react` and `react-dom`.

Navigate inside your `ionic-react-demo` project:

```bash
cd ionic-react-demo
```

Next, install the libraries from npm using the following command:

```bash
npm install --save react react-dom
```

## Adding JSX Support

Since React depends on using JSX templates, we'll also need to add JSX support to our project.

For this matter, we'll need to tweak the Webpack configuration file.

We'll also need to install some plugins for React using the following command:

```bash
npm install --save babel-loader babel-preset-react
```

Now open the `extra-webpack.config.js` file and instruct Webpack to associate the `.jsx` files with the `babel-loader` and react preset:

```js
const reactRule = [{
  test: /\.jsx$/,
  loader: "babel-loader",
  options: {
    presets: ['react']
  }
}];

module.exports = {
  module: {
    rules: reactRule
  }
}
```


Now you are ready to use React in your project!

## Updating index.html

Let's start by changing the `index.html` file. This is the initial content of this file:

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="UTF-8">
  <title>Ionic App</title>
  <meta name="viewport" content="viewport-fit=cover, width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <meta name="format-detection" content="telephone=no">
  <meta name="msapplication-tap-highlight" content="no">

  <link rel="icon" type="image/x-icon" href="assets/icon/favicon.ico">
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#4e8ef7">

  <!-- add to homescreen for ios -->
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black">

  <!-- cordova.js required for cordova apps (remove if not needed) -->
  <script src="cordova.js"></script>

  <!-- un-comment this code to enable service worker
  <script>
    if ('serviceWorker' in navigator) {
      navigator.serviceWorker.register('service-worker.js')
        .then(() => console.log('service worker installed'))
        .catch(err => console.error('Error', err));
    }
  </script>-->

  <link href="build/main.css" rel="stylesheet">

</head>
<body>

  <!-- Ionic's root component and where the app will load -->
  <ion-app></ion-app>

  <!-- The polyfills js is generated during the build process -->
  <script src="build/polyfills.js"></script>

  <!-- The vendor js is generated during the build process
       It contains all of the dependencies in node_modules -->
  <script src="build/vendor.js"></script>

  <!-- The main bundle js is generated during the build process -->
  <script src="build/main.js"></script>

</body>
</html>
```

We can safly remove the `<ion-app>` tag because this is an Angular component. We can also remove the the `<script>` tags because they are related to Angular. And let's import the Ionic v4 core library and add a root `<div>` where our React application will be mounted:


```html
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="UTF-8">
  <title>Ionic App</title>
  <meta name="viewport" content="viewport-fit=cover, width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <meta name="format-detection" content="telephone=no">
  <meta name="msapplication-tap-highlight" content="no">

  <link rel="icon" type="image/x-icon" href="assets/icon/favicon.ico">
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#4e8ef7">

  <!-- add to homescreen for ios -->
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black">
  <script src="https://unpkg.com/@ionic/core@4.0.0-beta.3/dist/ionic.js"></script>

  <!-- cordova.js required for cordova apps (remove if not needed) -->
  <script src="cordova.js"></script>

  <!-- un-comment this code to enable service worker
  <script>
    if ('serviceWorker' in navigator) {
      navigator.serviceWorker.register('service-worker.js')
        .then(() => console.log('service worker installed'))
        .catch(err => console.error('Error', err));
    }
  </script>-->

  <link href="build/main.css" rel="stylesheet">

</head>
<body>
  <div id="root"></div>
</body>
</html>
```

## Adding a React Component

Now let's create a React component that we can call `AppComponent` and mount the application:

First create the `app/AppComponent.jsx` file and add the following code:

```jsx
import React from 'react';

const AppComponent = props => {
  return (
    <div>
      Hello Ionic from React!
    </div>
  );
};

export default AppComponent;
```

Next, create the `main.jsx` file and add the following imports:

```js
import React, { Component } from "react";
import ReactDOM from "react-dom";
import AppComponent from "./app/AppComponent.jsx";

ReactDOM.render(
    <AppComponent/>
  ,document.getElementById("root")
);
```


We render the `AppComponent` which will be the root component of our application. You can create child components and the whole tree will be mounted.

## Conclusion

In this tutorial, we've seen a simple example of using React with Ionic v4.
