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
In package.json, change the main property
```
"main": "./client/index.jsx",
```

### Setup Webpack

```
npm install webpack webpack-cli webpack-dev-server html-webpack-plugin --save-dev
touch webpack.config.js
```
Add this to webpack.config.js
```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  mode: 'development',
  entry: path.join(__dirname, "client/src", "index.jsx"),
  output: {
    path:path.resolve(__dirname, "client/dist"),
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, "client/src", "index.html"),
    }),
  ],
  resolve: {
    extensions: ['', '.js', '.jsx']
  },
}
```

### Setup Babel

```
npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
```
Go to webpack.config.js and add the following code after output
```
module: {
    rules: [
      {
        test: /\.?(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react']
          }
        }
      },
    ]
  }
```
Your file should now look like this:
```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  mode: 'development',
  entry: path.join(__dirname, "client/src", "index.jsx"),
  output: {
    path:path.resolve(__dirname, "client/dist"),
  },
  module: {
    rules: [
      {
        test: /\.?(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react']
          }
        }
      }
    ]
  },
  resolve: {
    extensions: ['', '.js', '.jsx']
   },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, "client/src", "index.html"),
    }),
  ],
}
```

### Adding scripts to package.json

Add this to your package.json
```
"scripts": {
  "dev": "webpack serve",
  "build": "webpack"
}
```
Run locally
```
npm run dev
```
Build bundle
```
npm run build
```

### Setting up ESLint with AirBnB Style Guide and React

Install ESLint
```
npm install eslint --save-dev
```
To initialize:
MAC users
```
npx eslint --init
```
Windows
```
./node_modules/.bin/eslint --init
```
- How would you like to use ESLint? To check syntax, find problems, and enforce code style
- What type of modules does your project use? JavaScript modules (import/export)
- Which framework does your project use? React
- Does your project use TypeScript? No
- Where does your code run? Browser
- How would you like to define a style for your project? Use a popular style guide
- Which style guide do you want to follow? Airbnb (https://github.com/airbnb/javascript)
- What format do you want your config file to be in? JSON
- Would you like to install them now? Yes
- Which package manager do you want to use? npm

Add this to .eslintrc.json
```
"rules": {
"react/jsx-filename-extension": [1, {
"extensions": [".js", ".jsx"]}
]}
```
OPTIONAL:
```
touch .eslintignore
```
add to .eslintignore
```
webpack.config.js
```

### Jest & React Testing Library
Install React testing library dependencies
```
npm install --save-dev @testing-library/react @testing-library/jest-dom
```
Install Jest dependecies
```
npm install --save-dev jest jest-environment-jsdom
```
Configure Jest
In the terminal:
```
touch jest.config.js
```
add to jest.config.js
```
module.exports = {
    collectCoverage: true,
    collectCoverageFrom: ['src/**/*.{js,jsx}'],
    coverageDirectory: 'coverage',
    testEnvironment: 'jsdom',
}
```
In the terminal:
```
touch jest.setup.js
```
add to jest.setup.js
```
import '@testing-library/jest-dom'
```
go to jest.config.js
```
module.exports = {
  collectCoverage: true,
  collectCoverageFrom: ['src/**/*.{js,jsx}'],
  coverageDirectory: 'coverage',
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: ['<rootDir>/jest.setup.js'],
};
```
Integrate Jest with ESLint
```
npm install --save-dev eslint-plugin-jest
```
inside eslintrc.json edit the following properties
```
 "plugins": ["react", "jest"]
```
```
 "extends": [
        "plugin:react/recommended",
        "plugin:jest/recommended",
        "airbnb"
    ]
```
```
"env": {
        "browser": true,
        "es2021": true,
        "jest/globals": true
    }
```

make sure your eslintrc.json looks like this
```
{
    "env": {
        "browser": true,
        "es2021": true,
        "jest/globals": true
    },
    "extends": [
        "plugin:react/recommended",
        "plugin:jest/recommended",
        "airbnb"
    ],
    "overrides": [
    ],
    "parserOptions": {
        "ecmaVersion": "latest",
        "sourceType": "module"
    },
    "plugins": [
        "react",
        "jest"
    ],
    "rules": {
      "react/jsx-filename-extension": [1, {
        "extensions": [".js", ".jsx"]}
        ]
    }
}

```



Handy Sources:
Setup React with Webpack and Babel:
https://medium.com/age-of-awareness/setup-react-with-webpack-and-babel-5114a14a47e9#aa06

ESLint & AirBnB & React:
https://javascript.plainenglish.io/set-up-react-js-with-eslint-prettier-and-airbnb-cc015363a7c7

Jest:
https://dev.to/ivadyhabimana/setup-jest-and-react-testing-library-in-a-react-project-a-step-by-step-guide-1mf0
