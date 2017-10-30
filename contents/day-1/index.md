---
title: Geekwise Academy ReactJS
template: index.ejs
---

# Day 1: The Basics

## Who is everyone?

### About me

- I've been a web developer for about 4 years
- I work with Ruby, Rails, Angular, React, React Native and more
- I currently work for [FlexJobs](https://www.flexjobs.com) as a Senior Ruby on Rails Developer
- I co-founded [FermentAble, LLC](https://www.getfermentable.com)
  * Professional Brewery Management Software
  * Built with Ruby on Rails, GraphQL, and React
- Email: dphaener at gmail dot com
- Slack: https://geekwise.slack.com/messages/G7RGZ117H/

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

## Software/Frameworks

### React JS

We will of course be using [React JS](https://reactjs.org/) in this class.

### ES2015

It will be important to be up to speed on the most recent JavaScript
specification, ES2015. We will briefly cover some of the major changes and
things we will be using in this class in today's class.

### create-react-app

We will be using [create-react-app](https://github.com/facebookincubator/create-react-app)
to build the skeleton of our app and will follow many of the conventions that
are laid out in that skeleton (file structure, file naming, etc).

### Yarn

[Yarn](https://yarnpkg.com/) is a package manager for JavaScript. It acts as a
wrapper around NPM and you can install any package that is available via NPM
using Yarn. Yarn provides some extra features such as package caching and the
usage of a lockfile.

### GraphQL

The app that we will be building in class will have a data driven UI, so we
will need to be able to fetch data from and persist data to a remote server.
Instead of using a traditional REST API, we will be using [GraphQL](http://graphql.org/)
to accomplish this.

### Apollo Client

To make is easier to use GraphQL in our application, we will be using the
[Apollo Client](http://dev.apollodata.com/).

### Ramda JS

[Ramda JS](http://ramdajs.com/) is a functional programming library for
JavaScript. It is a lot like lo-dash or underscore on steriods. We will be using
this library here and there to make our lives easier.

### Jest

[Jest](https://facebook.github.io/jest/) is a test running framework that allows us to
easily run our tests and get output from the command line.

### Enzyme JS

[Enzyme JS](http://airbnb.io/enzyme/) is a testing framework built to make
testing React components easier. It was built and is maintained by the team at
[Airbnb](http://airbnb.io).

## Tools

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

We will be using Node 6.11.4 in this class. For those of you that do not have
node installed, let's get that done right now.

#### Mac OSX/Linux
I highly recommend using [NVM](https://github.com/creationix/nvm) to manage
and install your Node versions. Using homebrew you'll get an older version, which is
not what we want.

There are two ways to install NVM:
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.5/install.sh | bash
```
or
```bash
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.5/install.sh | bash
```

The script clones the nvm repository to `~/.nvm` and adds the source line
to your profile (`~/.bash_profile`, `~/.zshrc` or `~/.profile`).

Once you have successfully installed NVM, all you need to do now is install
node:
```bash
nvm install 6.11.4
```

#### Windows
You're on your own. Just kidding.

Go to the [NodeJS](https://nodejs.org/en/) website and download the installer.
Then use the installer to install Node.

## Getting Familiar with ES2015

Open up your terminal, make sure you're using the correct version of Node, and
fire up the REPL:
```bash
$ nvm use 6.11.4
Now using node v6.11.4 (npm v3.10.10)
$ node -v
$ node
>
```

### String Interpolation

ES2015 now supports string interpolation, meaning we no longer need to do this:

```js
var s = 'Foo' + bar + 'Baz';
```

Interpolation works by surrounding your string with backticks instead of
quotes.

```js
var s = `Foo ${bar} Baz`;
```

As you can see, we use the `${}` notation to interpolate. Anything inside
the brackets will be interpreted, so you can not only put variables inside,
but you can perform operations:

```js
console.log(`Four plus five equals ${4 + 5}`);
```

### Arrow Functions

Arrow functions are a shorthand for defining a function, plus as a bonus,
it automatically binds `this` to the function. So there's no more of this:

```js
this.number = 2;
var self = this;

var addNumbers = function(number) {
  return self.number + number;
}
```

That now simply becomes:

```js
this.number = 2;

var addNumbers = (number) => {
  return this.number + number;
}
```

Pretty neat huh?

If the function is just one line, you can write it like this:
```js
var addNumbers = (x) => (
  x + 2
);
```

Notice how we replaced the curly braces with parens? That means two things:
1. That the function can only have *one* line of code.
2. That the function is going to implicitly return the result of that one line.

So there's no need for a return. Awesome!

Also, if it's just a one liner like above, you can write that function like this:

```js
var addNumbers = x => x + 2;
addNumbers(2);
=> 4
```

We're going to see the first type of function used quite a bit in this class
in the form of `Functional Components` which will look something like this:

```js
const WelcomMessage = ({ name, message, sender }) => (
  <div>
    <span className='name'>Hello {name}</span>
    <span className='message'>{sender} wanted to tell you that {message}</span>
  </div>
);
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
let foo = { a: "1", b: "2" };
let { a, b } = foo;
console.log(a, b);
```

### Default Parameters

Another great feature of ES2015 is that you can define default parameters in
your function declarations. Take this code for example:

```js
var addNumbers = function(number, otherNumber) {
  if (otherNumber === undefined) {
    otherNumber = 2;
  }
  return number + otherNumber;
}
```

Using default parameters, we can now rewrite that like this:

```js
var addNumbers = function(number, otherNumber = 2) {
  return number + otherNumber;
}
```

### Spread Operators

Spread operators are another thing that come in extremely handy when
creating React components. I'll go over these briefly right now just so
we have a basic understanding.

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
  console.log(n);
}
```

Just a bit of really nice shorthand that makes looping easier.

### forEach and map

These are also a few that are already in browsers but don't get a lot of
attention.

```js
var a = [1, 2, 3];
a.forEach((num, index) => console.log(num, index));
```

```js
var a = [1, 2, 3];
a.map((num) => num + 1);
console.log(a);
```

### Classes

New in ES2015 is the ability to create your own classes. Classes support
inheritance, super calls, instance and static methods, and constructors.

Let's create a class that we can work with:

```js
class Car {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  name() {
    return `${this.year} ${this.make} ${this.model}`;
  }
}

let myCar = new Car("Toyota", "Highlander", "2003");
console.log(myCar.name());
```

You can also inherit from other classes. Let's make a new class called
`Vehicle` that will hold common information:

```js
class Vehicle {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  get name() {
    return `${this.year} ${this.make} ${this.model}`;
  }
}

class Car extends Vehicle {
  get type() {
    return 'Car';
  }
}

class Truck extends Vehicle {
  get type() {
    return 'Truck';
  }
}

let myCar = new Car("Toyota", "Highlander", "2003");
let myTruck = new Truck("Toyota", "Tacoma", "2005");

console.log(myCar.name);
console.log(myCar.type);
console.log(myTruck.name);
console.log(myTruck.type);
```


### Modules

In ES2015, we can easily import modules using, you guessed it, the `import` syntax.
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
$ yarn add global create-react-app
$ create-react-app todo
$ cd todo
$ yarn start
```

This will install all of the pre-requisites for a basic React app, including
React, React DOM, Babel, Webpack, and Nodemon.

Cool! We've got a basic hello world app ready to go!
