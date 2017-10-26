---
title: Geekwise Academy ReactJS
template: index.ejs
---

# Day 1: The Basics

## Who is everyone?

### About me

- I've been a web developer for about 2 1/2 years
- Started with Ruby/Rails, but have been full time (mostly) with React for the last 9 months
- I currently work for [Edit LLC](http://editllc.com/) doing a variety of things
- I have built an app called [FermentAble](https://www.getfermentable.com) that is using React on the front end
- Email: dphaener at gmail dot com
- Slack: https://geekwise-academy-frs.slack.com

### About Matt

- Web developer for almost 10 years
- Began with a focus on front end with HTML5, CSS3, and Javascript.
- Moved into Wordpress developement
- I work here at [Bitwise Industries](http://bitwiseindustries.com/) as a Developer Fellow leading a freelance cohort
- Email: mhigley at bitwiseindustries dot com

### Student Intros

- What's your name?
- What's your career background?
- What technologies do you have experience with?
- What do you hope to get out of this class?

## Tools

### ES6

We will be developing all of our React components using the new
[ES6](https://babeljs.io/docs/learn-es2015/) specification for JavaScript.
ES6 provides us with lot's of nifty new features that we'll be exploring
during this class.

This flavor of JS has not yet been adopted fully by most browsers, so
we will have to use [Babel](https://babeljs.io) to transpile our ES6 down
to browser compatible ES5.

### NPM

NPM is one of the package managers for JavaScript. It has a ton of modules
and is very well supported, so we will be using it for this class.

### Text Editor

Any text editor will do:

- I prefer Vim these days
- [Sublime Text](http://www.sublimetext.com/)
- [Atom](https://atom.io)

### Version Control (Git)

- We will be using Git + GitHub exclusively for version control in this course
- You don't have to be a git expert right off the bat
- Learn commands as you go, eventually you will "commit" them to memory (pun intended)
- Resources:
    - [Pro Git](http://git-scm.com/book) (free online book)
    - [Code School + GitHub's Try Git](http://try.github.io/) (interactive tutorial)
- Have we all heard of [GitHub](https://github.com)?

## Development Environment

### Node

We will be using Node 5.4 in this class. For those of you that do not have
node installed, let's get that done right now.

#### Mac OSX/Linux
I highly recommend using [NVM](https://github.com/creationix/nvm) to manage
and install your Node versions. Using homebrew you'll get 0.12.7, which is
not what we want.

There are two ways to install NVM:
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash
```
or
```bash
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash
```

The script clones the nvm repository to `~/.nvm` and adds the source line
to your profile (`~/.bash_profile`, `~/.zshrc` or `~/.profile`).

Once you have successfully installed NVM, all you need to do now is install
node:
```bash
nvm install 5.4
```

#### Windows
You're on your own. Just kidding.

Go to the [NodeJS](https://nodejs.org/en/) website and download the installer.
Then use the installer to install Node.

## Getting Started with ES6

Open up your terminal and fire up the Node REPL:
```bash
$ node $(node --v8-options | awk '/harmony/ && $1 ~ /^--/{print $1}')
```

That command will load all the harmony(ES6) options, which is needed for us to
be able to explore all of these things in the Node REPL.

If you're using Windows, this isn't going to work, so let's just grab the flags
that we need for today:

```bash
> node --harmony-destructuring --harmony-arrow-functions --harmony-default-parameters
```

### String Interpolation

ES6 now supports string interpolation, meaning we no longer need to do this:

```js
var s = 'Foo' + bar + 'Baz'
```

Interpolation works by surrounding your string with backticks instead of
quotes.

```js
var s = `Foo ${bar} Baz`
```

As you can see, we use the `${}` notation to interpolate. Anything inside
the brackets will be interpreted, so you can not only put variables inside,
but you can perform operations:

```js
console.log(`Four plus five equals ${4 + 5}`)
```

### Arrow Functions

Arrow functions are a shorthand for defining a function, plus as a bonus,
it automatically binds `this` to the function. So there's no more of this:

```js
this.number = 2
var self = this

var addNumbers = function(number) {
  return self.number + number
}
```

That now simply becomes:

```js
this.number = 2

var addNumbers = (number) => {
  return this.number + number
}
```

Pretty neat huh?

If the function is just one line, you can write it like this:
```js
var addNumbers = (x) => (
  x + 2
)
```

Notice how we replaced the curly braces with parens? That means two things:
1. That the function can only have *one* line of code.
2. That the function is going to implicitly return the result of that one line.

So there's no need for a return. Awesome!

Also, if it's just a one liner like above, you can write that function like this:

```js
var addNumbers = x => x + 2
addNumbers(2)
=> 4
```

We're going to see the first type of function used quite a bit in this class
in the form of `Function Components` which will look something like this:

```js
export default ({ name, message, sender }) => (
  <div>
    <span className='name'>Hello {name}</span>
    <span className='message'>{sender} wanted to tell you that {message}</span>
  </div>
)
```

That may look a bit weird right now, but by the end of this class you'll be
whipping out these stateless components like it's second nature.

### Destructuring

One of the weird things you may have noticed from the code sample above
is the function declaration:
```js
export default ({ name, message, sender }) => (
```

What we're doing there is called parameter destructuring. This function
expects an object to be passed in as a parameter that looks like:
```js
{
  name: 'Darin',
  message: 'You learned React',
  sender: 'Jason'
}
```

It will then assign the variables `name`, `message`, and `sender` to the
value of the keys in that object. If the keys don't exist, the variables
will be `undefined`.

Let's try it out in the REPL:
```js
let foo = { a: "1", b: "2" }
let { a, b } = foo
console.log(a, b)
```

### Default Parameters

Another great feature of ES6 is that you can define default parameters in
your function declarations. Take this code for example:

```js
var addNumbers = function(number, otherNumber) {
  if (otherNumber === undefined) otherNumber = 2
  return number + otherNumber
}
```

Using default parameters, we can now rewrite that like this:

```js
var addNumbers = function(number, otherNumber = 2) {
  return number + otherNumber
}
```

### Spread Operators

Spread operators are another thing that come in extremely handy when
creating React components. I'll go over these briefly right now just so
we have a basic understanging.

Imagine we have an object:
```js
var car = {
  make: 'Toyota',
  model: 'Corolla'
}
```

If we were to put this into a React component:
```js
<Car {...car} />
```

This would be the equivalent of saying:
```js
<Car make={car.make} model={car.model} />
```

It's just some nice, convenient shorthand that comes in quite handy in a lot
of cases. Especially in re-usable components.

### For..Of

This is another nice feature, that has actually made it's way into most
browsers already. It allows you to easily loop through an array:
```js
var a = [1, 2, 3]
for (var n of a) {
  console.log(n)
}
```

Just a bit of really nice shorthand that makes looping easier.

### forEach and map

These are also a few that are already in browsers but don't get a lot of
attention.

```js
var a = [1, 2, 3]
a.forEach((num, index) => console.log(num, index))
```

```js
var a = [1, 2, 3]
a.map((num) => num + 1)
console.log(a)
```

### Classes

New in ES6 is the ability to create your own classes. Classes support
inheritance, super calls, instance and static methods, and constructors.

Let's create a class that we can work with:

```js
class Car {
  constructor(make, model, year) {
    this.make = make
    this.model = model
    this.year = year
  }

  name() {
    return `${this.year} ${this.make} ${this.model}`
  }
}

let myCar = new Car("Toyota", "Highlander", "2003")
console.log(myCar.name())
```

You can also inherit from other classes. Let's make a new class called
`Vehicle` that will hold common information:

```js
class Vehicle {
  constructor(make, model, year) {
    this.make = make
    this.model = model
    this.year = year
  }

  get name() {
    return `${this.year} ${this.make} ${this.model}`
  }
}

class Car extends Vehicle {
  get type() {
    return 'Car'
  }
}

class Truck extends Vehicle {
  get type() {
    return 'Truck'
  }
}

let myCar = new Car("Toyota", "Highlander", "2003")
let myTruck = new Truck("Toyota", "Tacoma", "2005")

console.log(myCar.name)
console.log(myCar.type)
console.log(myTruck.name)
console.log(myTruck.type)
```


### Modules

In ES6, we can easily import modules using, you guessed it, the `import` syntax.
It looks something like this:

```js
import React from 'react'
```

So, the React module `exports` a `React` class, probably something like this:

```js
export default React
```

When we say `export default` in a module, we are saying that if you do not
specify which `export` to `import` (strange language, I know), then you'll
get the default. If we were to export things in this fashion:

```js
export default React

export Container
```

Then we could import like this:

```js
import React, { Container } from 'react'
```

Yup, you can use destructuring during an import too. Awesome!

## Getting Started With React

### Dependencies and a development server

We've covered the basics so let's get started with some React! Let's just
create a small sample application to get us started. Go to whatever directory
you like to keep your code in and make a new directory called `todo`. Change
into that directory and let's get started by installing some modules.

```bash
$ mkdir todo
$ cd todo
$ npm init --yes
$ npm install -g webpack
$ npm install --save react react-dom
$ npm install --save babel babel-core babel-loader
$ npm install --save babel-preset-es2015 babel-preset-react babel-preset-stage-0
$ npm install --save webpack webpack-dev-server react-hot-loader
```

This is all of the packages that we'll need to get going. Let's break down what
we've done here.

First we installed webpack globally. We won't need this immediately, but we will
want to be able to use the webpack CLI later on, so it's a good idea to have it
installed this way.


Next we installed React. You'll notice that it now comes in two packages. As of
React 0.14.x the team over at Facebook decided to split React up into two modules.
The `React` contains most of the core logic, while the `ReactDOM` library
is mostly used for rendering. This was done in order to be able to handle
rendering React elements across multiple platforms (think [React Native](https://facebook.github.io/react-native/)).

Ok cool, we've got React installed, but now we need to be able to transpile all
of our code down to ES5. We're going to be using [Webpack](https://webpack.github.io/)
to bundle up all of our assets and transpile the ES6 and JSX code we'll be writing
down to plain old ES5. But Webpack can't do it alone. That's why we installed
all of those Babel modules. They all help us to compile our code properly so
that we can write beautiful code with the new ES6 and JSX syntax, but still
have our code be compatible on most browsers (I'm looking at you IE8).

Last but not least, we installed the Webpack development server and React hot
loader so we can run a hot reloading development server. What's that mean? It
means that we can edit our code (Javascript and CSS) and the updates will
be reflected in the browser without refreshing the page (most of the time).

Cool! We just need a little bit more configuration and we'll be ablle to get
our development server up and running. Just copy and paste the following code
into a file in the root of your app directory called `webpack.config.js`

```js
var webpack = require('webpack');

module.exports = {
  entry: {
    'app': [
      'webpack-dev-server/client?http://localhost:8881/',
      'webpack/hot/only-dev-server',
      './app.jsx'
    ]
  },
  output: {
    path: __dirname,
    filename: "[name].js",
    publicPath: 'http://localhost:8881/',
    chunkFilename: '[id].chunk.js',
    sourceMapFilename: '[name].map'
  },
  resolve: {
    extensions: ['', '.js', '.jsx', '.es6'],
    modulesDirectories: ['node_modules']
  },
  module: {
    loaders: [
      { test: /\.jsx$|\.es6$|\.js$/, loaders: ['react-hot', 'babel-loader'], exclude: /node_modules/ },
      { test: /\.scss$|\.css$/, loader: 'style-loader!style!css!sass' }
    ]
  },
  plugins: [
    new webpack.NoErrorsPlugin()
  ],
  devtool: "eval-source-map"
};
```

This is our Webpack configuration file, and it's just telling webpack where to
find the code that we cant to compile, and how to do it. Let's go through it
piece by piece.

The first entry is well, the entry. This defines a list of entry points that
Webpack will look for when compiling our code. An entry point is simply a file
that Webpack opens and looks for dependencies. Webpack is pretty smart when
compiling code for us. It will traverse through all of the dependencies that we
request and create one optimized bundle that doesn't duplicate any dependencies
so we can be certain that ouro bundle is highly optimized.

The second entry is where we tell Webpack how we want to output our bundle. In
this case, we're serving up our bundled assets on our local server. Keep in mind
that this is only for development, and we'll be using the Webpack CLI later to
bundle our assets for deployment.

The resolve entry tells Webpack to look for certain file extensions when
resolving module dependencies so that we don't have to include the file extension
in the `import` declarations. It's also telling Webpack where our modules are
located, so that it doesn't traverse those directories when creating bundles.

The next entry defines which loaders to use (Webpack requires that we have
specific loaders installed in order to be able to process specific types of files,
which is why we installed the Babel loader and all of it's individual modules
earlier). It simply uses a regular expression to see if a filename matches, and
if so uses the appropriate loader to process that file.

Beyond that, we're telling Webpack which plugins we want to use, and then
telling it that we want to use the source map dev tool so that in the console
we can actually look at our original source code for debugging instead of the
transpiled code.

That's it! Now we can write some code!

### Some actual code!

Let's begin by creating a basic HTML page that we'll use to display our
React components. In the root of your app, let's create a file called `index.html`
and just paste in the following code:

```html
<html>
  <head>
    <title>Hello React</title>
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body>
    <div id="react"></div>
    <script src="/app.js"></script>
  </body>
</html>
```

This is just a basic template that's going to load up Bootstrap and give us a
place to mount our React components.

Next let's create our first React component. Open up another new file called
`app.jsx`, also in the root of your app folder and put in the following code:

```js
import React from 'react'
import ReactDOM from 'react-dom'

class App extends React.Component {
  render() {
    return (
      <div className='container'>
        Hello World!
      </div>
    )
  }
}

ReactDOM.render(<App />, document.getElementById('react'))
```

Cool! We've got a basic hello world app ready to go! Let's take a look at what's
happening here. We're using class based components in this class, so whenever
you create a component, you have to inherit from the base `React.Component` class.
This gives you all of the methods that a basic React class has, which we'll be diving
into a bunch more as the class progresses.

Every React component must have a `render` method. It can return `null`, or it
can return JSX. [JSX](https://facebook.github.io/react/docs/jsx-in-depth.html)
is what we'll be using to represent our DOM. JSX is a syntax that allows us
to write HTML like code in our React components. Babel then transpiles our
JSX down into plain Javascript. You don't have to use JSX to write your React
components, but it makes it much easier to read and reason about.

One thing to note, is that you can only return one DOM node in the render method.
So this won't work:

```js
return (
  <div>Foo</div>
  <div>Bar</div>
)
```

### Let's make this thing dynamic

React is all about making amazingly fast, dynamic UI's, so let's do that shall we?

Let's take out our `Hello World` code and add in some dynamic code! Completely
replace your render method so that it looks like this:

```js
render() {
  const { name } = this.state

  return (
    <div className='container'>
      <label>What's your name</label>
      <input type='text' onChange={this.updateName} defaultValue={name} />
      <p>Your name is {name}</p>
    </div>
  )
}
```

So what we've done here is add a simple text input with an `onChange` callback
that's going to allow us to dynamically change the value of the `name` variable
inside the paragraph. Let's implement the initial state in the constructor of
our class and also the `updateName` method.

```js
class App extends React.Component {
  constructor(props) {
    super(props)

    this.state = { name: props.name }
  }

  updateName = (ev) => {
    const { value } = ev.target
    this.setState({ name: value })
  }
}
```

We did it! What's happening here is that we're setting the initial state of our
component with the `name` prop that is passed in (which currently is NOT being
passed in). Then when the input is changed, we're updating the state of our
component to match the new name value from the input. When `setState` is called
in a React component, it triggers a refresh of the component, and the magic of
the Virtual DOM and DOM diffing is enacted and the UI is updated. We'll discuss
the Virtual DOM in the next class in detail.
