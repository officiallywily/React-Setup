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
Add this to the index.jsx
```
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './components/App';

ReactDOM.createRoot(document.getElementById('root')).render(<App />);
```
Add this to the App.jsx
```
import React from 'react';

function App() {
  return <h1>Hello I Am App</h1>;
}

export default App;
```

### Setup Webpack

```
npm install webpack webpack-cli webpack-dev-server --save-dev
npm install html-webpack-plugin --save-dev
touch webpack.config.js
```
Add this to webpack.config.js
```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: path.join(__dirname, "client/src", "index.jsx"),
  output: {
    path:path.resolve(__dirname, "client/dist"),
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, "client/src", "index.html"),
    }),
  ],
}
```
