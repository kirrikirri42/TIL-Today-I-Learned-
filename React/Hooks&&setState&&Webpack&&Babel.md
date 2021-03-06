# TIL-Today-I-Learned- 20200616(Tue)

## Hooks
https://www.youtube.com/watch?v=EUQnxfZgFJU&list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&index=11

- `Hook` Using Refs, setStates and useEffects in function components

- setState is Asynchronous 

- It's better to use functions in setState if we're using previous states to get new states.

- Cannot use `class` and `for` in React because React also has elements under those names.
So use `className` and `htmlFor` instead

https://www.youtube.com/watch?v=ZyOOdGBqZbk&list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&index=12

### setState class vs Hooks 
In class type, setState can either set all the states, or parts of the them.
```
this.setState((prevState) => {
    return {
        result: prevState.value + ':정답',
        first: Math.ceil(Math.random() * 9),
        second: Math.ceil(Math.random() * 9),
        value: '',
    };
});
```

```
this.setState({
    result: '땡',
    value: '',
    });
```

However, in Hooks, setState should always set all the states because otherwise, the nonstated ones will lose their values.
So states are better declared separately like below:

```
const [first, setFirst] = React.useState(Math.ceil(Math.random() * 9));
const [second, setSecond] = React.useState(Math.ceil(Math.random() * 9));
const [value, setValue] = React.useState('');
const [result, setResult] = React.useState('');
const inputRef = React.useRef(null);
```

- Rendering only occurs once even though several states are declared separately because setStates are asynchronous


# Webpack
## Install
https://www.youtube.com/watch?v=66_D4RYpFqY&list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&index=13

- In html script, only one JavaScript file can be used as source. But it's hard to put all the components in one JavaScript file (because it's too long and hard to see)
- Web pack solves this problem by combining several JavaScript files into one.
- It can edit codes (ex. remove console.logs)
- Can apply Babal/text
- Must know Node.js to use Web pack because it's JavaScript (Node.js is JavaScript executor)

`npm init` in a directory will create `package.json`

`npm i react react-dom`

`npm i -D webpack webpack-cli` install webpack -D means for development purposes

in packages.json, webpack will be placed under "devDependencies" section because it's not used for services

## webpack.config.js, client.jsx, WordRelay.jsx, index.html
### webpack.config.js

```
const path = require('path'); // Import Node.js' path controller

module.exports = {
    name: 'word-relay-setting', // Any name. Unnecessary option
    mode: 'development', // For real service:production
    devtool: 'eval', // Fast. "hidden-source-map" for real service
    resolve: {
        extensions: ['.js', '.jsx'] // No need to write .js or .jsx for files under entry
    },

    // Important part
    entry: {
        app: ['./client'], // Files to make the output file. If files are imported in another file, they don't need to be written down here. 'WordRelay.jsx' is imported in 'client.jsx'
    },
    
    module: {
        rules: [{
            test: /\.jsx?/,
            loader: 'babel-loader',
            options: {
                presets: ['@babel/preset-env', '@babel/preset-react'],
                plugins: ['@babel/plugin-proposal-class-properties'],
            },
        }],
    },
    
    output: {
        path: path.join(__dirname, 'dist'), // Set's the path to <current directory>/dist
        filename: 'app.js'  //output file
    },
};
```

### client.jsx
```
const React = require('react');
const ReactDom = require('react-dom');

const WordRelay = require('./WordRelay');

ReactDom.render(<WordRelay />, document.querySelector('#root'));
```
No need to import using <scripts> due to the first two lines
Better to write *.jsx instead of *.js if using jsx grammar because it immediately tells that it's a React file.


### WordRelay.jsx
Creating WordRelay game
 
```
const React = require('react');
const { Component } = React;

class WordRelay extends React.Component {
    state = {
        text: 'Hello, webpack',
    };
    render() {
        return <h1>{this.state.text}</h1>;
    }
}

module.exports = WordRelay; // To use it outside
```
The first two lines to import React libraries and packages
The last part allows the component to be used outside by importing like below:
`const WordRelay = require('./WordRelay');


### index.html

```
<html>
    <head>
        <meta charset="UTF-8" />
        <title>끝말잇기</title>
    </head>
    <body>
        <div id="root"></div>
        <script src="./dist/app.js"></script> // bring app.js
    </body>
</html>
```

## Babel
Webpack cannot read jsx if Babel is not installed
`npm i -D @babel/core` basic babel

`npm i -D @babel/preset-env` preset that allows my computer to use the lastest JavaScript

`npm i -D @babel/preset-react` allows to use jsx

`npm i -D babel-loader` links babel to webpack

`npm i -D @babel/plugin-proposal-class-properties` to use state


- The following codes in webpack.config.js show modules (better to place it between entry and output)
```
    module: { //These modules are applied to the entries to produce outputs
        rules: [{
            test: /\.jsx?/, // Regular expression. Apply rules to js and jsx files
            loader: 'babel-loader', // which rule
            options: { // Babel option
                presets: ['@babel/preset-env', '@babel/preset-react'], // names of presets
                plugins: ['@babel/plugin-proposal-class-properties'],
            },
       }],
    },
```
 
## Run webpack
Running webpack creates 'app.js' in 'dist' directory. (shown in the code above)

Writing `webpack` doesn't do anything in the terminal because `webpack` has not been registered as a command.

Solution:

1. In package.json file write the comman as scripts:
```
"scripts": {
  "dev": "webpack"
},
```
`npm run dev`

2. Enter `npx webpack` in terminal



## GuGuDan
client.jsx, webpack.config.js, index.html are same as those above except names.
GuGuDan.jsx file is based on the Hooks GuGuDan with minor modifications

```
const React = require('react');
const { useState, useRef } = React; // This allows us to remove React that was infront of useState

const GuGuDan = () => {
    const [first, setFirst] = useState(Math.ceil(Math.random() * 9));
    const [second, setSecond] = useState(Math.ceil(Math.random() * 9));
    const [value, setValue] = useState('');
    const [result, setResult] = useState('');
    const inputRef = useRef(null);

    const onSubmitForm = (e) => {
        e.preventDefault();
        if (parseInt(value) === first * second) {
            setResult((prevResult) => {
                return value + ': 정답'
            });
            setFirst(Math.ceil(Math.random() * 9));
            setSecond(Math.ceil(Math.random() * 9));
            setValue('');
            inputRef.current.focus();
        } else {
            setResult('땡');
            setValue('');
            inputRef.current.focus();
        }
    };

    const onChangeInput = (e) => {
        setValue(e.target.value);
    };

    return (
        <> // React.Fragment can be removed as well
            <div>{first} 곱하기 {second}는?</div>
            <form onSubmit={onSubmitForm}>
                <input ref={inputRef} onChange={onChangeInput} value={value} />
                <button>입력!</button>
            </form>
            <div id="result">{result}</div>
        </>
    );
}

module.exports = GuGuDan;
```
