# About
This is a simple react-app without create-react-app

### Steps
#### 1. Creating the folder
```bash
mkdir react-setup
cd react-setup
```

#### 2. Setting up npm package
```bash
npm init -y
```
You will see a `package.json` file being generated in the `react-setup` directory.

#### 3. Installing React
Now after setting up with the `package.json` file, we will installing `react` and `react-dom`.
```bash
npm install react react-dom
```
This create a folder `node_modules/` and a file `package-lock.json`.

#### 4. Installing babel
```bash
npm install @babel/core @babel/preset-env @babel/preset-react babel-loader
```

#### 5. Setting up Babel File
Create a file in the root directory by the name `.babelrc` and inside it paste the following code:
```json
{
    "presets": ["@babel/preset-react", "@babel/preset-env"]
}
```

#### 6. Installing Webpack
```bash
npm install webpack webpack-cli webpack-dev-server
npm install html-webpack-plugin
```

#### 7. Connecting the webpack to babel
Create a file in the root directory by the name `webpack.config.js` and paste the following code inside it:
```js
const HtmlWebpackPlugin = require("html-webpack-plugin");
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.[hash].js",
    path: path.resolve(__dirname, "dist"),
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
  resolve: {
    modules: [__dirname, "src", "node_modules"],
    extensions: ["*", ".js", ".jsx", ".tsx", ".ts"],
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: require.resolve("babel-loader"),
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.png|svg|jpg|gif$/,
        use: ["file-loader"],
      },
    ],
  },
};
```
If we take a look at the above code, out entry file is an `index.js` in a `src/` folder. So first we create a folder by the name of `src` and create an `index.js` file.

#### 8. Creating Files
Create a folder named `src` and inside create the following files.
1. *index.js:*
```js
import React from 'react'
import ReactDom from 'react-dom'
import App from './App'

ReactDom.render(<App />, document.querySelector("#root"));
```

2. *App.js:*
```js
import React from 'react'

function App() {
    return (
        <div>
            Hello World!! 🚀🚀
        </div>
    )
}

export default App
```

3. *index.html:*
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React App</title>
</head>
<body>
    <div id="root"></div>
</body>
</html>
```

#### 9. Setting up Webpack
Open the `package-json` file and go-to *scripts*, replce the original script object with this:
```json
"scripts": {
    "start": "webpack-dev-server --hot --open --mode development",
    "build": "webpack --config webpack.config.js --mode production"
}
```

#### 10. Installing CSS & Image Plugins
```bash
npm install --dev style-loader css-loader file-loader
```

#### 11. Final
Now make a basic React App and run `npm start` and on your app will run on `localhost:8080`.