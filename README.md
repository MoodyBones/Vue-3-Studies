# Vue 3 Studies

- 🚌&nbsp;&nbsp; Course on [Frontend Masters](https://frontendmasters.com/courses/vue-3/)
- 👩‍🏫&nbsp;&nbsp; Taught by [Sarah Drasner](https://twitter.com/sarah_edo)
- 📓&nbsp;&nbsp; Notes by [Mel Jones](https://twitter.com/_moodybones)
- 📎&nbsp;&nbsp; Link to [Starter Docs](https://github.com/sdras/intro-to-vue)
- 🔮&nbsp;&nbsp; Start date: 2020/11/04 - yikes what a day to be alive!

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

# Day 2 - Directives continued

### v-if / v-if-else

- Conditionally render siblings

### v-bind or :

- For class and style bindings, creating dynamic props and more.
- It's a very popular directive so it comes with a shortcut!

### v-for

- loops through a set of values
- can also do a static number

```html
// you can grab more than one property // and write dynamic keys
<p v-for="(value, key, index) in jokes" :key="`key-${index}-${value}`">
  {{ index }}. {{ key }}: {{ value }}
</p>

data() { return { jokes: { question: 'What do you call a boomerand that won't
come back?', answer: 'A stick', response: 'ROFL', } } }
```

```js
// Static Number
<ul class="">
  <li v-for="num in 5" :key="num">{{ num }}</li>
</ul>


```

# Day 3 - Directives Cont.

### v-once & v-pre

- v-once will not update once it's been rendered
- v-pre will print out the inner text exactly how it is, including code (good for documentation)

`{{$data}}`

- this will print whatever is in data
- great if you want to quickly check something fast, without opening dev tools
- like a respnse from a server

### v-on or @

- extremely useful, so there is a shortcut for
- great for binding events like click and mouseenter
- you can pass in a parameter for the event (param)
- you can also use ternaries directly
- you can haev multiple bindings

Example of multiple bindings

```html
<div
  v-on="
  mousedown: doThis,
  mouseup: doThat
"
></div>
```

- this is great if you want to build games in Vue
- because you can have a click and key event at the same time

### v-html

- great for stringd that have html elements that need to be rendered

warning

- do not accept user input and then put it to the page with `v-html`
- incase you don't know what you're getting. you could get hacked.

### v-text

- similar to using the mustache template
- use case for when you don't access to the mustache template and want to add to insert something inside a tag
- If you want to dynamically update things then it is recommend that you use the mustache template because it is updated a little faster.

## id

- it needs to be unique to the DOM
- best practice is to use a library that will generate unique IDs
- uuid

## modifiers

### v-model.trim

- Will string any leading or trailing whitespace from the bound string

### v-model.number

- changes strings to numbers

### v-model.lazy

- won't populate the content automatically, it will wait to bind until an even happens. It listens to change events instead of input
- it is used a lot to aid in performance
- and is used for input validation

### @mousemove.stop

- is comparable to e.stopPropagation()

### @mousemove.prevent

- is comparable to e.preventDefault()

### @submit.prevent

- will no longer reload the page on submission

### @click.once

- do not confuse it with v-once
- this click event will be triggered once

### @click.native

- for listening to native evnts in the DOM

## Keycodes

- Vue 3 uses names instead of numbers for the Keycodes
- this is because the HTML spec has changed and is deprecating the use of numbered keycodes

# Day 4 - Methods

## Methods

- Are bound to the Vue instance
- Incredibly useful for functions you would like to access in Directives
- They can also be access in other parts, like lifecycle hooks, other methods, computed properties

- **When you look at the Vue instance and the options API - that data is an object**
- Methods are functions that hang off the Vue Instance Object!
- `this` is this case, is always referring to the data

### Creative Coding in Javascript

- If you want to make generative colors
- Hue values are very good for this
- Because Hue is a big circle and so it won't ever fail
- and you can keep going round, unlike hex or rbg where you'll hit an end

Writing Vue is very declarative

- we are holding state
- we are changing the state in some way
- and then we are out putting it to the page

Codepen: [Methods - hold state, change state, output to page](https://codepen.io/MoodyBones/pen/ZEOmMbM)

# Day 5 - Methods in Forms

## Methods in Forms

- [Codepen Example](https://codepen.io/MoodyBones/pen/VwjqpmY)
- challenge is to create a form that posts to a server
- server we will use: typicode json placeholder - it's great if you need to get some fake server responses to make sure things are evaluating correctly

`@submit.prevent="submitForm"` will prevent the form from reloading the page on submission

- use [Vuelidate](https://vuelidate.js.org/) for form validation

```html
<h1>Nina Simone Top 10</h1>
<div>
  <span>Sort by</span>
  <button @click="sortLowest">Lowest rated</button>
  <button @click="sortHighest">Highest rated</button>
</div>
<article>
  <table>
    <tr>
      <th v-for="key in columns">{{ key }}</th>
    </tr>
    <tbody>
      <tr v-for="entry in ratingsInfo">
        <td v-for="key in columns">{{ entry[key] }}</td>
      </tr>
    </tbody>
  </table>
</article>
```

```js
data() {
    return {
      columns: ["title", "rating"], // this makes it easy to rename in the future
      ratingsInfo: [
        { title: "Feeling Good", rating: 1 },
        { title: "My Baby Just Cares For Me", rating: 2 },
        { title: "I Put A Spell On You", rating: 3 },
        ...
      ]
    };
  },
  methods: {
    sortHighest() {
      this.ratingsInfo.sort((a, b) => (a.rating > b.rating ? 1 : -1));
    },
    sortLowest() {
      this.ratingsInfo.sort((a, b) => (a.rating < b.rating ? 1 : -1));
    }
  }
```

- `this` binding is very important
- We want to establish a relationship with properties
- Ee can not use an arrow function at the top level
- because it would not create the binding!!
- e.g. `sortLower() => {}` will not create the binding

# Day 6 - Computed

## Computed

- Computed properties are calculations that will be cached and
- will only update when needed

- Highly performant but use with understanding

- Computed properties give us a new view onto that data
- you are not mutating data
- but we are able to do something with the data and return a different value to it
- it will on be reevaluated or recalculated when the data is changed - so it's very performant

```js
const App = {
  data() {
    return {
      userData: '',
    }
  },
  computed: {
    greeting() {
      return `You're a monster, ${this.userData}!`
    },
  },
}
// it looks like a method but its not
// use it like data
// remember you are putting a new view of that data
```

## Computed vs Methods

Computed

- Runs only when a dependency has changed
- Cached - this can be a gotcha, and you may need to use a method instead!
- **Should be used as a property, in place of data**
- are a new view on the data
- By default getter only. but you can define a setter
- you can filter through large amounts of data without any dependencies - is a big strength of computed properties

Methods

- Runs whenever an update occurs
- Not cached
- Are typically invoked from v-on/@, but flexible
- getter/setter

# Day 7 - Computed cont.

- Computed is great for search
- it's in the place of the data
- you can filter large amounts of data peformantly
- use regex for filtering data

## Exercises

- a form with 3 inputs and 1 button
  - heading "Add a new post"
  - input "title"
  - input "author name"
  - dropdown input "Add a new label"
  - button "Add a new blog post"
- dropdown "Filter by label"

<!-- # Day 8 -  -->
<!-- # Day 9 -  -->
<!-- # Day 10 -  -->

### Huge thanks to Sarah Drasner & the Frontend Masters Team.
