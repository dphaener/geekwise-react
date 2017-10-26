---
title: Geekwise Academy ReactJS
template: index.ejs
---

# Day 2: React vs. Angular

## Similarities

## Differences

# React Basics

## The Virtual DOM

The [Virtual DOM](https://facebook.github.io/react/docs/glossary.html) is
something that you'll hear a lot about in the React community and sounds a bit
weird at first. But it's nothing to be afraid of. It's something that has been
around for awhile, and is by no means unique to React. React, however uses it
heavily and it's the reason for it being so fast.

Simply speaking, it's a representation of the actual DOM in memory. When
React renders your components on the page, it creates a Virtual copy of it in
memory. When updates are triggered via `setState` or other methods, React creates
a copy of the new DOM in memory, and performs a diff. It then only updates what
has changed. This is far more fast and efficient than traversing the actual DOM
and updating it in place.

## Reusable Components

It is more often than not desirable to be able to create React components that
are reusable. React is great for this and you can find the full documentation
of everything we're going to cover right now here: https://facebook.github.io/react/docs/reusable-components.html.

### Prop Types

When creating reusable components, it's a good idea to use [propTyes to validate
the input coming into the component, and to raise errors when required props
are not passed in.

```js
class MyComponent extends React.Component {
  static propTypes = {
    name: PropTypes.string,
    email: PropTypes.string.isRequired
  }
}
```

In the above example, if the component is not given a `name` prop, React will
print out a warning in the console. However, if the `email` prop is not supplied,
an error will be raised.

### Default props

If you'd like to have default values for props, you can do that too:

```js
class MyComponent extends React.Component {
  static defaultProps = {
    classes: 'inline'
  }
}
```

This way, if somebody creates this component without passing the `classes` prop
we know it will have some value, but if the prop is supplied, it will use the
supplied value instead.

### React Router

We'll be using [React Router](https://github.com/rackt/react-router) for all of
our routing needs.

Exercise:

`Install React Router and get the basic routing up and running with an index page`

### Flux Architecture

We'll be using the [Flux](https://facebook.github.io/flux/docs/overview.html)
application architecture for handling application state.

Our implementaion of choice for Flux will be [Redux](https://github.com/rackt/redux)

Let's install Redux, and Redux React
