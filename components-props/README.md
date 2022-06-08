# Vue 3 Studies - Components, Props, Slots

- 🚌&nbsp;&nbsp; Course on [Frontend Masters](https://frontendmasters.com/courses/vue-3/)
- 👩‍🏫&nbsp;&nbsp; Taught by [Sarah Drasner](https://twitter.com/sarah_edo)
- 📓&nbsp;&nbsp; Notes by [Mel Jones](https://twitter.com/_moodybones)
- 📎&nbsp;&nbsp; Link to [GitHub Starter Docs & Slides](https://github.com/sdras/intro-to-vue)

# Codepen links to ALL my Vue 3 Collections

- [Directives](https://codepen.io/collection/nGrgGW)
- [Exercises/Challenges](https://codepen.io/collection/DrRLoJ)
- [Methods](https://codepen.io/collection/nmomeM)

# Components

- there are multiple ways of declaring Vue components
- they are very flexible
- not all are useful
- simpler ones are not as useful
- complex means with a CLI & a build tool

## Templates

- Vue uses HTML based template syntax to bind the Vue instance to the DOM, very useful for components
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
;<div class="app">
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

**Vue is a progressive framework, so we support incremental adoption**

### Slightly better component with props

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
  props: ['text'], // empty shell -  can name it whatever you want
  template: `<div>{{ text }}</div>`
})

app.mount('#app')

```

# Props

- Props down & Events up
- Passing data down from the parent to the child
- the parent should own the state, and the child is just receiving it
- think it like the child is holding a variable and waiting on the parent to send it down
- Props are intended for one way communication

### Types & Validation

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

**Objects and arrays need their defaults to be returned from a function:**

```js
text: {
  type: Array,
  default: function () {
    return ['al pastor', 'carne asada']
  }
}

// or with an arrow
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

# Components

- [slides](https://slides.com/sdrasner/intro-to-vue-3-3?token=NLsRwMvr)
- Each component instance has its own isolated scope
- Data must be a function.
- In Vue 2 you could make a choice to make it an function or not, depending on the scope you wanted
- In Vue 3 all components have theie own isolated scope
- If you don't make it a functon it can affect the data of all other instances
- [Docs example](https://vuejs.org/v2/guide/components.html#data-Must-Be-a-Function)

## camelCasing

- Vue knows that html has no camel case attributes
- It will convert them all to kebab-case
- you can still use it JavaScript

```html
// camelCasing props: ['booleanValue'] // in HTML it will be kebab-case
<checkbox :boolean-value="booleanValue"></checkbox>
```

```js
const app = Vue.createApp({
  data() {
    return {
      newComment: '',
      comments: [
        'Looks great Julianne!',
        'I love the sea',
        'Where are you at?',
      ],
    }
  },
  methods: {
    addComment() {
      this.comments.push(this.newComment)
      this.newComment = ''
    },
  },
})

app.component('individual-comment', {
  template: `<li> {{ commentpost }} </li>`,
  props: ['commentpost'],
})

app.mount('#app')
```

```html
<ul>
  <individual-comment
    v-for="comment in comments"
    :key="comment"
    :commentpost="comment"
  >
  </individual-comment>
</ul>
<input
  v-model="newComment"
  @keyup.enter="addComment"
  placeholder="Add a comment"
/>
```

### Ordering

- You can't put the app.component before you declar the Vue.createApp()
- This is different in Vue 3!

## Individual Script Component x-template

- If you can't use single file Components
- you can create them in script tags
- then reference with the id
- [link to Sarah's codepen](https://codepen.io/sdras/pen/xxZeRyg?editors=0010)

```js
// put at bottom of html, see Sarah's example if confused
<script type="text/x-template" id="comment-template">
<li>
	<img class="post-img" :src="commentpost.authorImg" />
  <small>{{ commentpost.author }}</small>
  <p class="post-comment">"{{ commentpost.text }}"</p>
</li>
</script>

// and this in JS file
app.component('individual-comment', {
  template: '#comment-template', // here you can reference the id of the component x -template
  props: ['commentpost']
})

```

### A smart component

- methods
- render stuff
- [Sarah's example](https://codepen.io/sdras/pen/2751def77693975f59bc72a237f1ba89)

**App**

```js
const app = Vue.createApp({
  data() {
    return {
      manifest: [
        {
          item: 'backpack',
          url: 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/28963/backpack.jpg',
        },
        {
          item: 'tshirt',
          url: 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/28963/tshirt.jpg',
        },
        {
          item: 'sweatshirt',
          url: 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/28963/sweatshirt.jpg',
        },
      ],
    }
  },
})
```

```html
<div id="app">
  <div class="unit" v-for="unit in manifest" :key="unit.item">
    <app-child :item="unit.item" :url="unit.url"></app-child>
  </div>
</div>
```

**Component**

```js
app.component('app-child', {
  template: '#child',
  props: ['item', 'url'],
  data() {
    return {
      counter: 0,
    }
  },
})
```

```html
<div class="item">
  <h2>{{ item }}</h2>
  <img :src="url" width="235" height="300" />
  <div class="quantity">
    <button class="inc" @click="counter > 0 ? counter -= 1 : 0">-</button>
    <span class="quant-text">Quantity: {{ counter }}</span>
    <button class="inc" @click="counter += 1">+</button>
  </div>
  <button class="submit">Submit</button>
</div>
<!--item-->
```

## Communicating Events with emit

- A way to report activity from the child to the parent
- the child doesnt change/mutate it
- the child tells the parent, so the parent can update item
- One way flow of data so there is only one source of truth
- _This is one way to do it, we will explore other cases with Vuex and Composition API_
- when you see $ thats something Vue is offering us
- [See codepen example](https://codepen.io/sdras/pen/6a0a49ff73cd3c49f14b83d63a9ffd00)
- in the example they have different names, but you can name them the same

```js
const app = Vue.createApp({
  data() {
    return {
      text: 'where is my taco...',
    }
  },
  methods: {
    updateTaco() {
      this.text = '🌮!'
    },
  },
})

app.component('order-button', {
  template: '#order-button',
})

app.mount('#app')
```

```html
<div id="app">
  <div>
    <h2>{{ text }}</h2>

    <order-button @gettaco="updateTaco"></order-button>
  </div>
</div>

<script type="text/x-template" id="order-button">
  <button @click="$emit('gettaco')"> <!-- here it emit's to the parent, it has no state of it's own -->
    Click me to order a taco
  </button>
</script>
```

### $emit - Passing params

- you can pass params
- for example you can use it has a count/quanity in an online shop
- [see on codepen](https://codepen.io/sdras/pen/666f76cb09ab151c13b551a552ed2996)

```html
<my-component @myevent="parentHandler"></my-component>

<button @click="$emit('myevent', param)"></button>
```

# Slots

- like passing props,
- but for cases when you need to render content differently
- Pass some content into a component with ease
- A modal is good example, because the modal might change

```html
<div id="app">
  <h3>Let's trigger this here modal!</h3>
  <button @click="toggleShow">
    <span v-if="isShowing">Hide child</span>
    <span v-else>Show child</span>
  </button>

  <app-modal v-if="isShowing">
    <!-- instead of closing the component immediately -->
    <!-- we can add whatever we want because our template below has a slot -->
    <h2>Here I am!</h2>
    <button @click="toggleShow">Close</button>
  </app-modal>
</div>

<script type="text/x-template" id="modalcomponent">
  <div class="modal">
  <slot></slot> <!-- here we can write a slot, so that above we add whatever we want -->
  </div>
</script>
```

### Slots can have defaults

`<slot>I am some default text</slot>`

### You can give Slots names

- Naming slot templates are different in Vue 3 than past versions
- `v-slot:header` is new
- if you forget to name a slot it still works

```html
<template v-slot:header>
  <h1>Taco Blog</h1>
</template>

<header>
  <slot name="header"></slot>
</header>
```

Sarahs Slot Codepen examples

- [Modal Codepen example](https://codepen.io/sdras/pen/cfd942c61930f8b4e04507cabf4939c9?editors=1000)
- [Content Codepen example](https://codepen.io/sdras/pen/e06f9393e73054e7185ff48dfa36e161)
- [named / no named slot example](https://codepen.io/sdras/pen/bd5bcb6c54654770994ad02d0b3194d4)
- [wine label example](https://codepen.io/sdras/pen/bd5bcb6c54654770994ad02d0b3194d4) | Wine label is very cool

From the wine bottle example

```html
<component :is="selected">
  ...
  <path
    class="label"
    d="M12,295.9s56.5,5,137.6,0V409S78.1,423.6,12,409Z"
    transform="translate(-12 -13.8)"
    :style="{ fill: labelColor }"
  />
</component>

<h4>Color</h4>
<button @click="selected ='appBlack', labelColor = '#000000'">
  Black Label
</button>
<button @click="selected ='appWhite', labelColor = '#ffffff'">
  White Label
</button>
<input type="color" v-model="labelColor" defaultValue="#ff0000" />
```

# :is Directive & keep alive

- allows you to have dynamic components
- you can pass in whatever you want and switch out components as we need
- wrap that component in keep-alive
- keep alive remembers which component has been mounted
- the inactive component gets cached and will be there when you return
- it remembers which piece was dynamically bound
- [Sarah's example](https://codepen.io/sdras/pen/bd394c76a0aa9e44abc37e3d061aef1b)

```html
<keep-alive>
  <component :is="selected"> // ... </component>
</keep-alive>
```

Theres a lot more to scoped slots, [so check out the documentation](https://v3.vuejs.org/guide/component-slots.html#scoped-slots)

# Components Exercise

### [Link to my repo](https://codepen.io/MoodyBones/pen/OJRzoqd)

TODOS

- HTML is already formatted
- Data has a locations
- create a component
- pass in all the data
- find a place to use a slot - do this second

### Huge thanks to Sarah Drasner & the Frontend Masters Team.
