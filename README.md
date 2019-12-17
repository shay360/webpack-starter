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

### To work with multiple pages and bundles change the output to:
```javacsript
 entry: {
        index: './src/index.js',
    },
    output: {
        filename: "[name].bundle.js",
        path: path.resolve(__dirname, 'www/dist')
    },
```

## commit #6 - Add loader for css and scss
In this commit we are adding loaders to work with css and scss.<br>
The basic steps are:
1. npm install the loader
2. set the rule for using the loader in webpack.config.js<br>
:bowtie: rule is an object inside rules Array
```javascript
mode: 'none',
    module: {
        rules: [
            {
                // This is a rule object
            }
        ]
    }
```
> So how we writing the rule for css and scss

I want to tell him to use the loaders on any .css file
```javascript
rules: [
            {
                test: /\.css$/,
                use: [
                    'style-loader', 'css-loader'
                ]
            }
        ]
```
> Now lets write rule for scss

I want to tell him to use the loaders on any .scss file
```javascript
{
    test: /\.scss$/,
    use: [
        'style-loader', 'css-loader', 'sass-loader'
    ]
}
```

##### A little word on use Array:
The use array in webpack will be read from right to left so in the scss example it will first use `sass-loader`


### After we set the rules for the css and scss it's time to install them thru npm
`npm install style-loader css-loader sass-loader node-sass --save`
###### use --save and not --save-dev

## commit #7 - Add Babel to the project

The steps to setup babel in the project.
1. write a new rule to handel js files in webpack.config.js, the rule will include the preset and all configurations for babel
```javascript
{
    test: /\.js$/,
    exclude: /node_modules/,
    use: {
        loader: 'babel-loader',
        options: {
            presets: ['@babel/env'],
            plugins: ['transform-class-properties']
        }
    }
}
```
2. install the required loaders and babel package<br>
`npm install @babel/core babel-loader @babel/preset-env babel-plugin-transform-class-properties --save-dev`

> #### Congratulations you can start work with the download of the commit #7

## commit #8 - Adding minification plugin to the webpack result
In this commit we will install a plugin to make this work
> To add plugin array to the project you need to add 'plugins' to the webpack.config.js
```javascript
 mode: 'none',
    plugins: [],
```

So now you can set the plugin in a few steps:
> Add it to the plugins array
```javascript
 plugins: [
        new TerserPlugin()
    ],
```
> Import the plugin in the top of the file
```javascript
const path = require('path');
const TerserPlugin = require('terser-webpack-plugin');
``` 
> Install the plugin
`npm install terser-webpack-plugin --save-dev`

## commit #9 - Adding jQuery to the project
For adding jQuery you need to run<br>
`npm install jquery`
The you can import him to the project thru the index.js<br>
> You have two options to import it.

#### The babel way (ES6)
import $ from "jquery";

#### The webpack way
var $ = require("jquery");

## commit #10 - Adding Bootstrap to the project
Now we will add bootstrap to the project and import him.<br>
`npm install bootstrap` will install the npm package of bootstrap <br>
Now you need to install proper.js and if you dont have jquery installed so install it now see commit #9
`npm install popper.js --save`<br>
Now you can start do some imports in the index.js
```javascript
import $ from "jquery";
import 'bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css'

```








