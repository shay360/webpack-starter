# webpack-starter
## commit #1 - Add basic files and directories
### Basic Project Files
* ./dist/
* ./dist/index.html
* ./src/
* ./src/index.js
* ./src/components/
* ./src/components/hello-world-component/
* ./src/components/hello-world-component/hello-world-component.js
* ./src/components/hello-world-component/hello-world-component.scss

### Basic GIT files
.gitignore
.README.md<br>
.gitignore need to ignore:
```javascript
.idea/
node_modules/
```

## commit #2 - Add NPM package.json
`npm init`
You can use `npm init -y` to make it quick and skip questions

## commit #3 - Add Webpack to our project
Use the npm to install webpack into our project. <br>
For installing the webpack you ned to install 2 things
1. webpack
2. webpack-cli<br>
 ** Use the --save-dev command**<br>
`npm install webpack webpack-cli --save-dev`

## commit #4 - Add webpack configuration file
Add new file to the project folder called webpack.config.js<br>
This is the default name oof file that webpack will search for.<br>
In this file you need to write all you configuration include the rules of webpack.

## commit #5 - Make general configuration for webpack
> In this commit we are working on 3 files,
1. webpack.config.js
2. package.json<br>
3. index.html

> package.json

in file package.json you need to change the scripts->test parameter, you dont need him.<br>


```javascript
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
Change to:
```javascript
"scripts": {
    "build": "npx webview -w"
  },
```

that will tell npm to build allways thru the webpack builder and the -w command says it will watch <br>
####A little word on building.
you can build the prject by one of the following:
1. npm run build -> that command will use the scripts->build
2. npx webpack / -w -> that command is the webpack command to build, the -w option is to watch files

> webpack.config.js

In this file we will config some basic configurations to work with webpack
```javascript
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        filename: "bundle.js",
        path: path.resolve(__dirname, 'dist')
    },
    mode: 'none'
}
```
We are creating a module configuring the next:
1. entry: where is the js file we need to compile via webpack
2. output: where and how to bundled file will be called and storage, in this case ./dist/bundle.js
3. mode -> for our basic configuration just add 'none' but you can use: `'production' / 'development'`

> index.html

In this file all we need to to is to import the bundle.js
```html
<body>

<script src="bundle.js"></script>
</body>
</html>
```
##### Now you can run `npx webview` and check if there are no errors and bundle.js is built

