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

Form

```html
<form @submit.prevent="addPost">
  <button type="submit"></button>
</form>
```

# Day 8 - Differences in Vue 2 & 3: Filters

- Surface API is the same
- reactivity system in different in Vue 3
- New Advanced Compisition API
- deprecated filters
- because you can do everything with a computed property instead
- they wanted to make Vue 3 smaller

**You can't pass params with computed properties, but you can with methods**

### Computed is good for:

- Adding currency
- Dates 1st 2nd etc
- filtering large maount of data based on user input
- creating data visualizations you can explore

## Watcher & Vue's Reactivity System

to dive in deeper - how vue 3 uses reactivity
it's important for debugging or to understand how things update

### What is reactive?

- "Reactive programming is programming with asynchrouns data streams"
- frameworks that use it: RxJs, Angular, Vue, MobEx
- **"A stream is sequence of ongoing events ordered in time that offer some hooks with which to observe it"**
- "When we use reactive premises for building applications, this means it's very easy to update state in reaction to events."

e.g. a hover state that has a transition, theres the moment that you hover on it, then the transition state in which it's changing, and then the end state

You have hooks in which you can observe the start, the transition & the end part.

In Frontend development we are mostly reacting to state change
To dive further [Andre Staltz post](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)

### How does Vue3 do This

- Detect when theres a change in one the values
- Track the function that changes it
- Trigger the function so it can update the final value

## Proxies

- are a new JS feature
- It is "An Object that encases another object or functions and allows you to intercept it."

`new Proxy(target, handler)`

### Basic Proxy Syntax

```js
const dinner = {
  meal: 'tacos',
}

const handler = {
  get(target, prop) {
    return target[prop]
  },
}

const proxy = new Proxy(dinner, handler)
console.log(proxy.meal)
// tacos
```

### Intercepted

```js
const dinner = {
  meal: 'tacos',
}

const handler = {
  get(target, prop) {
    console.log('intercepted!') // we can intercept it
    return target[prop]
  },
}

const proxy = new Proxy(dinner, handler)
console.log(proxy.meal)
// tacos
// intercepted!
```

### JS trap

```js
const dinner = {
  meal: 'tacos',
}

const handler = {
  get(target, prop) {
    // This a trap in Javascript
    console.log(`We swapped out your dinner`)
    return 'burger' // we return a burger instead
  },
}

const proxy = new Proxy(dinner, handler)
console.log(proxy.meal)
// burger
```

### Use Reflect to bind `this` properly

```js
const dinner = {
  meal: 'tacos',
}

const handler = {
  get(target, prop, receiver) {
    return Reflect.get(...arguments) // this is vanilla js
  },
}
// Use Reflect to bind `this` properly

const proxy = new Proxy(dinner, handler)
console.log(proxy.meal)
// tacos
```

### Track the things changing we can intercept

- This is important when using watchers
- because we want to track what dependencies are changing during the process

```js
const dinner = {
  meal: 'tacos',
}

const handler = {
  get(target, prop, receiver) {
    track(target, prop) // a function that will collect and track the info
    return Reflect.get(...arguments) // and still return
  },
}

const proxy = new Proxy(dinner, handler)
console.log(proxy.meal)
// tacos
```

### Get & Set

- remember computed properties are only get only (not set)
- we're able to track all the properties that are changing
- then trigger a new function that will update things accordingly
- trigger in Vue runs the changes

```js
const dinner = {
  meal: tacos,
}

const handler = {
  get(target, prop, receiver) {
    track(target, prop)
    return Reflect.get(...arguments)
  },
  set(target, key, value, receiver) {
    trigger(target, key)
    return Reflect.set(...arguments)
  },
}

const proxy = new Proxy(dinner, handler)
console.log(proxy.meal)
```

### If the value is the same then don't do stuff

```js
const dinner = {
  meal: tacos,
}

const handler = {
  get(target, prop, receiver) {
    track(target, prop)
    return Reflect.get(...arguments)
  },
  set(target, key, value, receiver) {
    let oldValue = target[key]
    let result = Reflect.set(...arguments)
    if (oldValue != result) {
      trigger(target, key)
    }
    return result
  },
}
```

~~Detect when theres a change in one of the values~~ Proxies do this automaticiall for us
**Track** the function that changes it
**Trigger** the function so it can update the final value

### Other Vue 3 Reactivity Notes

- in Vue 2 everything was all together,
- in Vue 3 everything became very tree shakable and we're doing code splitting, a few other things
- That means that everything exists in seperate packages - reactivity, templates, transitions are all seperate
- so if you're not using one of them, it will get rid of it, then you get a smaller build

To explore further go to: github/com/vuejs/vue-next/tree/master/packages/reactivity
Proxies are ES6 (previously Object.defineProperty)

# Day 9 - Watchers

## Watchers

- Good for asynchronous updates
- updates/transitions on data changes
- Watch any data property that we created
- the data the watcher can have the same name

```js
data() {
  return {
    counter: 0
  },
},
watch: {
  counter() {
    console.log(`the data has changed`)
  }
}
```

- we are hooking into the reactivity sysytem
- whenever something chnaged, please let us know
- it gives a layer we can intercept or change

**We also have access to the new value and the old value**

```js
watch: {
  watchedProperty(newValue, oldValue) {
    // your code goes here
  }
}
```

- if you have a data visualization
- and you want to animate a the part between the new and the old you can

**We can gain access to nested values**

```js
watch: {
  watchedProperty {
    deep: true,
    watchedProperty(newValue, oldValue) {
    // your code goes here
    }
  }
}
```

```js
data() {
  return {
    counter: 0
  },
},
watch: {
  counter(newValue, oldValue) {
    console.log(`the data has changed, it was ${oldValue} it is now ${newValue}`)
  }
}
```

[Check out this cool pen of Sarah's](https://codepen.io/sdras/pen/dRqZOy)

- when you scroll to the bottom it triggers a call to the api to return more beers

```js
const App = {
  data() {
    return {
      bottom: false,
      beers: [],
    }
  },
  watch: {
    bottom(newValue) {
      if (newValue) {
        this.addBeer()
      }
    },
  },
  created() {
    // lifecycle hook, as soon as this is created start listening to the scroll
    window.addEventListener('scroll', () => {
      this.bottom = this.bottomVisible() // this.bottom calls this.bottomVisible
    })
    this.addBeer()
  },
  methods: {
    bottomVisible() {
      // we are evaluating the scroll height and returning whether or not we've hit the bottom
      const scrollY = window.scrollY
      const visible = document.documentElement.clientHeight
      const pageHeight = document.documentElement.scrollHeight
      const bottomOfPage = visible + scrollY >= pageHeight
      return bottomOfPage || pageHeight < visible
    },
    addBeer() {
      // using axios to get more beers
      axios.get('https://api.punkapi.com/v2/beers/random').then((response) => {
        let api = response.data[0]
        let apiInfo = {
          name: api.name,
          desc: api.description,
          img: api.image_url,
          tips: api.brewers_tips,
          tagline: api.tagline,
          food: api.food_pairing,
        }
        this.beers.push(apiInfo) // pushes into beers array
        if (this.bottomVisible()) {
          this.addBeer()
        }
      })
    },
  },
}

Vue.createApp(App).mount('#app')
```

**When watching a property you trigger a method on change**

```js
data() {
  return {
    bottom: false,
    beers: []
  }
},
watch: {
  bottom(newValue) {
    if (newValue) {
      this.addBeer();
    }
  }
}

```

```html
<div id="app">
  <section>
    <h1>🍺 Make yourself some Punk Beers 🍻</h1>
    <div v-if="!beers.length" class="loading">Loading...</div>
    <!-- use v-if Loading if waiting on an api -->
    <div v-for="beer in beers" class="beer-contain">
      <div class="beer-img">
        <img :src="beer.img" height="350" />
      </div>
      <div class="beer-info">
        <h2>{{ beer.name }}</h2>
        <p class="bright">{{ beer.tagline }}</p>
        <p><span class="bright">Description:</span> {{ beer.desc }}</p>
        <p><span class="bright">Tips:</span> {{ beer.tips }}</p>
        <h3 class="bright">Food Pairings</h3>
        <ul>
          <li v-for="item in beer.food">{{ item }}</li>
        </ul>
      </div>
    </div>
  </section>
</div>
```

You don't have to build your own scroller, you can use this one build by a Vue core team member
[Vue Virtual Scroller](https://github.com/Akryum/vue-virtual-scroller)

- fast
- lazy

[You can change data sets based on Watchers](https://codepen.io/sdras/pen/OWZRZL?TB_iframe=true&width=370.8&height=658.8)

# Day 10 - Watchers Exercise

ToDO

- Use a watcher to change one of the values
- Pay attention to the set timeout
- watchers are good with API's - asynch functions/ when returnin data
- ask a question "Is it nice out today?"
- click button to find out
- return [yesno wtf api](https://yesno.wtf/#)
- also conditionally render an emoji & bg change
  😎
  👎
  🙃

### yesno wtf api

```js
{
  "answer": "yes",
  "forced": false,
  "image": "https://yesno.wtf/assets/yes/2.gif"
}

```

PARAMS: force
TYPE: string
DESCRIPTION: Force answer, can be yes, no or maybe

[My Solution](https://codepen.io/MoodyBones/pen/KKgvyRP)

```js
<template>
  <div id="app">
    <p>Is it nice out today?</p>
    <button
      @click="getAnswer"
    >
      Click to find out
    </button>
    <div>{{ answer }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      answer: '',
      buttonClicked: 0,
      yes: '😎',
      no: '👎',
      maybe: '🙃'
    };
  },
  watch: {
    answer(newValue, oldValue) {
      if (newValue) {
        console.log(`the data has changed, it was ${oldValue} it is now ${newValue}`)
        if (newValue === 'yes') {
            this.answer = this.yes
          } else if (newValue === 'no') {
            this.answer = this.no
          } else if (newValue === 'maybe') {
            this.answer = this.maybe
          }
      }
    }
  },
  methods: {
    increment() {
      this.buttonClicked++
    },
    getAnswer() {
      this.answer = 'Thinking...'
      axios
        .get('https://yesno.wtf/api')
        .then(response => {
            this.answer = response.data.answer
       })
       .catch(error => {
            this.answer = 'Error! Could not reach the API. ' + error
        })

    }
  }
};
</script>
```

Sarah's Solution with setTimeout to reset

```js
<template>
  <div id="app">
    <button
      @click="getTaco"
    >
      Click me to order a taco
    </button>
    <div>{{ orderStatus }}</div>
    <div v-if="orderSubmitted">{{ orderSubmitted }}</div>
  </div>
</template>


data() {
  return {
    orderStatus: 'where is my taco...',
    orderSubmitted: null
  }
},
methods: {
  getTaco() {
    this.orderStatus = '🌮!'
  }
},
watch: {
  orderStatus(newValue, oldValue) {
    this.orderSubmitted = 'your order was submitted!';

    setTimeout(() => this.orderSubmitted = null, 1000) // turns back to null after 1 second
  }
}
```

**Watchers are great for watching for change and then doing an animation**
[Check out this pen](https://codepen.io/sdras/pen/RZGqxR)

- we can watch the beginning values & end values
- we can change them

### Watchers changing other things

- you can only watch one thing
- but in that thing you can change other things by
  - calling a method
  - when you see something has changed, then you can change a different piece of data
- if you are looking at one thing and changing another it's called a side effect!!!
  - you are changing something that someone else doesn't really know about
  - this is not good practice
  - it's better to encapsulate things in methods and call the method
  - this is different from computed properties, because computed allows you a view on a piece of data
  - where watchers allow you to affect multiple pieces

# Components

- there are multiple ways of declaring Vue components
- they are very flexible
- not all are useful
- simpler ones are not as uselful

## Templates

- Vue used HTML based template syntax to bind the Vue instance to the DOM, very useful for components
- Templates are optional, you can also write render function with JSX support

### the different types

- Strings (only useful for small cases)
- Script tags
- Single file components (most common use case in a Vue app)

### Strings (only useful for small cases)

```js

//js
const App = {
  template = '<h1>hello world</h1>'
}
Vue.createApp(App).mount('#app')
```

Why use components in a Vue app?

- it makes things clearer and easier to understand

## Components

- A collection of elements that are encapsulated into a group that can be accessed through one single element
- Makes traversing and maintaining code easier and more legible

#### Simplest Component

```js
;<div class="App">
  <p>{{ message }}</p>
  <component-a />
</div>

const app = Vue.createApp({
  data() {
    return {
      message: 'hi from parent',
    }
  },
})

//because we have named the above app
app.component('component-a', {
  template: <p>hi from child</p>,
})

app.mount('#app')
```

#### Slightly better component with props

```js
<div id="app">
  <div>
    <h2>Every time you see a child component, you have to give me a taco</h2>
    <app-child :text="message"></app-child> // : === v-bind
    <app-child :text="message"></app-child>
    <app-child :text="message"></app-child>
  </div>
</div>

const app = Vue.createApp({
  data() {
    return {
      message: 'Give me a taco!'
    }
  }
})

app.component('app-child', {
  props: ['text'],
  template: `<div>{{ text }}</div>`
})

app.mount('#app')

```

## Props

- Props down & Events up
- Padssing data down from the parent to the child
- the parent should own the state, and the child is just receiving it
- think it like the child is holding a variable and waiting on the parent to send it down
- Props are intended for one way communication

#### Types & Validation

```js
app.component('app-child', {
  props: {
    text: {
      type: String,
      required: true,
      default: 'hello mr. magoo',
    },
  },
  template: `<div>{{ text }}<div>`,
})
```

- if you put the wrong type, it won't break the code, it'll just give you warnings in dev mode

**Objects and arrays need their defaults to be returned from a function: **

```js
text: {
  type: Array,
  default: function () {
    return ['al pastor', 'carne asada']
  }
}

text: {
  type: Array,
  default: () => ['al pastor', 'carne asada']
}
```

You don't need to necessarily pass the data in props to the child, either, you have the option of using vue instance data or a static value as you see fit:

https://codepen.io/sdras/pen/5a34f6ed12cf954202c6d38f1ceba633

Not using the state of the parent
`<child count="1"></child>`

vs

Using the state of the parent
`<child :count="count"></child>`

We use v-bind or : to dynamically bind props to data on the parent

**Each component instance has its own isolated scope, data must be a function.**

camelCasing will be converted
props: ['booleanValue']

In HTML it will be kebab-case:
<checkbox :boolean-value="booleanValue"></checkbox>

### Individual Script Component x-template

- if you can't use single file Components
- you can create them in script tags
- then reference with the id

```js
<script type="text/x-template" id="comment-template">
<li>
	<img class="post-img" :src="commentpost.authorImg" />
  <small>{{ commentpost.author }}</small>
  <p class="post-comment">"{{ commentpost.text }}"</p>
</li>
</script>

app.component('individual-comment', {
  template: '#comment-template', // here you can reference the id
  props: ['commentpost']
})


```

### Huge thanks to Sarah Drasner & the Frontend Masters Team.
