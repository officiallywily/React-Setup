# React Setup Guide

## Set up React with Babel, Webpack, Eslint/AirBnB style guide, Jest/React testing library

### Setup React and folder system

```
npm init -y
mkdir client
mkdir client/src
mkdir client/src/components
touch client/src/index.html
touch client/src/index.jsx
touch client/src/components/App.jsx
npm install react react-dom
```

Add this to the index.html we just created
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```
Add this to the index.js
```
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './components/App';

ReactDOM.createRoot(document.getElementById('root')).render(<App />);
```
