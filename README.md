# Vue 3 Studies

- 🚌&nbsp;&nbsp; Course on [Frontend Masters](https://frontendmasters.com/courses/vue-3/)
- 👩‍🏫&nbsp;&nbsp; Taught by [Sarah Drasner](https://twitter.com/sarah_edo)
- 📓&nbsp;&nbsp; Notes by [Mel Jones](https://twitter.com/_moodybones)
- 📎&nbsp;&nbsp; Link to [Starter Docs](https://github.com/sdras/intro-to-vue)
- 🔮&nbsp;&nbsp; Start date: 2020/11/04 - yikes what a day to be alive!

## I am creating a [Vue 3 cheatsheet](https://codepen.io/collection/nGrgGW) on CodePen as I learn

- [v-model](https://codepen.io/MoodyBones/pen/pobKMMR)
- [v-if/v-show](https://codepen.io/MoodyBones/pen/vYKaEXj)

# Day 1 - Introduction & Resources

## Why

- Declarative / setting a few things and little the computer do the hard work
- Legible
- Easy to maintain
- Powerful
- A collection of the best of the best / other frameworks
- Elegant
- Gives me what I want when I need it, and gets out of my way
- A way to be really productive

### Comparison with other frameworks

- A virtual DOM
- Reactive components that offer the View layer only.Like Angular, not React.
- Props and a centralized state management stor similar to React
- Conditional rendering, and services, similar to Angular
- Inspired by Polymer for simplicity and performance. Vue offers a similar development style as HTML, styles and JavaScript are composed in tandem
- Scoped styles - similar to styled components in React

## New Features in Vue 3

- conditional API

## Vue Instance

- use id because you only want one instance

## Vanilla JS vs Vue

Vanilla JS

```js
const items = ['thingie', 'another thingie', 'something else', 'bla blah']

function listOfStuff() {
  const full_list = items.map((el) => `<li> ${el} </li>`)

  const contain = document.querySelector('#container')
  contain.innerHTML = `<ul> ${full_list} </ul>`
}

listOfStuff()
```

Vue

- it's very declarative
- we are holding the state and telling the DOM what to do with it.
- can write semantic html
- reactive - responding to changes in state

```js
const App = {
  data() {
    return {
      items: ['thingie', 'another thingie', 'something else', 'bla blah'],
    }
  },
}
```

```html
<div id="#app">
  <ul>
    <li v-for"item in items">
      {{ item }}
    </li>
  </ul>
</div>

```

# Directives

v-if
v-else
v-else-is
v-show
v-for
v-text
v-HTML
v-slot
v-on
v-bind
v-model
v-pre
v-cloak
v-once

## v-model

- Creates a relationship between the data in the instance/component AND a form input
- So that you can dynamically update values
- two way binding

## v-if / v-show

- is a conditional that will display information depending on meeting a requirement.
- This can be anything - buttons, forms, divs, components

### v-if

- if you check in the dev tools you will see
  `<!--v-if-->`
- then when it evaluates to true it will mount the element/button/component
- if that is toggled often, it can be expensive
- and then it's better to use `v-show`

### v-show

- if you check in the dev tools you will see:
- the element/button/component has been mounted, WITH style: none
- alternatively if you have a big component, and you don't want it loaded and chilling in the DOM all the time,
- then it's better to use `v-if`

<!-- # Day 2 -  -->
<!-- # Day 3 -  -->
<!-- # Day 4 -  -->
<!-- # Day 5 -  -->

### Huge thanks to Sarah Drasner & the Frontend Masters Team.
