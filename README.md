# Vue 3 Studies

- 🚌&nbsp;&nbsp; Course on [Frontend Masters](https://frontendmasters.com/courses/vue-3/)
- 👩‍🏫&nbsp;&nbsp; Taught by [Sarah Drasner](https://twitter.com/sarah_edo)
- 📓&nbsp;&nbsp; Notes by [Mel Jones](https://twitter.com/_moodybones)
- 📎&nbsp;&nbsp; Link to [GitHub Starter Docs & Slides](https://github.com/sdras/intro-to-vue)
- 🔮&nbsp;&nbsp; Start date: 2020/11/04 - yikes what a day to be alive!

## Quick Folder Links

- [Directives / Modifiers / Data rendering](directives-modifiers-data-rendering/README.md)
- [Methods / Computed / Watchers / Reactivity](methods-computed-watchers/README.md)
- [Components, Props, Slots](components-props/README.md)
- [App Development / Nuxt / Vue CLI](app-development-nuxt/README.md)

## I have created a [Vue 3 Directives cheatsheet](https://codepen.io/collection/nGrgGW) on CodePen

- [v-model](https://codepen.io/MoodyBones/pen/pobKMMR)
- [v-if/v-show](https://codepen.io/MoodyBones/pen/vYKaEXj)
- [v-if/v-else-if](https://codepen.io/MoodyBones/pen/yLJqENg)
- [v-bind or :](https://codepen.io/MoodyBones/pen/qBNyyoO)
- [v-for - static number](https://codepen.io/MoodyBones/pen/JjKBaWW)
- [v-for - object](https://codepen.io/MoodyBones/pen/MWeBPem)
- [v-once & v-pre](https://codepen.io/MoodyBones/pen/PozdZpB)
- [v-on or @](https://codepen.io/MoodyBones/pen/XWKPdrR)
- [v-html](https://codepen.io/MoodyBones/pen/LYZJbPd)
- [v-text](https://codepen.io/MoodyBones/pen/mdEGOwY)
- [Directives Exercise](https://codepen.io/MoodyBones/pen/oNLPYmO)

- and a bunch more pens!!

# Codepen links to ALL my Vue 3 Collections

- [Directives](https://codepen.io/collection/nGrgGW)
- [Exercises/Challenges](https://codepen.io/collection/DrRLoJ)
- [Methods](https://codepen.io/collection/nmomeM)

# Introduction & Resources

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

### Huge thanks to Sarah Drasner & the Frontend Masters Team.
