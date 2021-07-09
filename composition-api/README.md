### Options API is not deprecated.

## Composition API is an add on.

previously we used mixins and the composition api helps us move away from that

It's a common situation: you have two components that are pretty similar, they share the same basic functionality, but there's enough that's different about each of them that you come to a crossroads: do I split this component into two different components? Or do I keep one component, but create enough variance with props that I can alter each one?

# **ENTER COMPOSITION API.**

- we can compose it

Thank you Functional Progamming

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1434c3b4-ca43-45bf-ae75-3a46b2f0544b/Screen_Shot_2021-07-09_at_14.06.08.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1434c3b4-ca43-45bf-ae75-3a46b2f0544b/Screen_Shot_2021-07-09_at_14.06.08.png)

> Composition API allows you to encapsulate one piece of functionality so that you can use it in different components throughout the application.
> If written correctly, they are pure- they don't modify or change things outside of the function's scope, so you will reliably always receive the same value with the same inputs on multiple executions.

It makes the returns very clean / clear - thank your FP [Functional Programming](https://www.notion.so/Functional-Programming-731c643782de4adf9859d2675c586f31)

### It is based on React hooks

see viz tweet [https://twitter.com/prchdk/status/1056960391543062528?s=20](https://twitter.com/prchdk/status/1056960391543062528?s=20)

### Before

[https://codepen.io/sdras/pen/ed762c954ff67f56c47de955b754805c](https://codepen.io/sdras/pen/ed762c954ff67f56c47de955b754805c)

```jsx
const App = {
  data() {
    return {
      tacos: '',
    }
  },
}

Vue.createApp(App).mount('#app')
```

### With Composotion API

[https://codepen.io/sdras/pen/45492786305a158d50f5264867959343](https://codepen.io/sdras/pen/45492786305a158d50f5264867959343)

```jsx
const { ref } = Vue

const App = {
  // similar to data
  setup() {
    const tacos = ref('') // set to empty string

    // implicit return
    return {
      tacos,
    }
  },
}

Vue.createApp(App).mount('#app')
```

- html stay the same

### Why is this an advanced feature? Why change things?

- mixins - one couldn't consume another
- great for resuable logic:
  - getting dimensions of the viewport and component
  - gathering specific mousemove events
  - base elements of charts
  - clipboards
  - media queries
  - dark mode

Can also be put in a seperate js file with the template part

## ref

- We use ref in template the same, but if we use it in a function, we would extract with taco.value

```jsx
const count = ref(0)

function increment() {
  count.value++
}
```

Rather than writing methods (that hang off of the vue instance) - we now write functions

## reactive

- If we use reactive, we no longer have to use .value to use the value elsewhere. A little more familiar, similar to data in options

```jsx
const state = reactive({
  count: 0,
})

function increment() {
  state.count++
}
```

- Instead of declaring `refs` repeatedly
- create a reactive object
- you don't have to call it state (but it is current best practice)

### Example using ref

[https://codepen.io/sdras/pen/e4af9bf8f7795704ef584eb909d03424](https://codepen.io/sdras/pen/e4af9bf8f7795704ef584eb909d03424)

```jsx
const { ref } = Vue

const App = {
  setup() {
    const restaurantName = ref(`Let's taco bout it`),
      options = ref(['Lengua', 'Carnitas', 'Al Pastor', 'Pollo']),
      numItems = ref(0),
      deliveryTime = ref(25),
      freeDelivery = true

    function addItems() {
      numItems.value++
    }

    return {
      restaurantName,
      options,
      numItems,
      deliveryTime,
      freeDelivery,
      addItems,
    }
  },
}

Vue.createApp(App).mount('#app')
```

### Example using Reactive

[https://codepen.io/sdras/pen/b50f1e800a5f3b8b47392c2d2d66c2bd](https://codepen.io/sdras/pen/b50f1e800a5f3b8b47392c2d2d66c2bd)

```jsx
const { reactive, toRefs } = Vue

const App = {
  setup() {
    const state = reactive({
      restaurantName: `Let's taco bout it`,
      options: ['Lengua', 'Carnitas', 'Al Pastor', 'Pollo'],
      numItems: 0,
      deliveryTime: 25,
      freeDelivery: true,
    })

    function addItems() {
      state.numItems++
    }

    return {
      ...toRefs(state),
      addItems,
    }
  },
}
```

- instead having to declare all the pieces
- or putting `ref` everywhere
- we spread state into `toRefs`
- which also means when you reference them you no longer had to say `state.options` or `state.freeDelivery`
- instead you can say `options` or `freeDelivery`

## Computed Properties

```jsx
setup() {
  const state = reactive({
    count: 0,
    double: computed(() => state.count * 2)
  })

  return {
    state
  }
}
```

## Watch

```jsx
setup() {
  const state = reactive({
    count: 0
  })

  watch(state, (newValue, oldValue) => {
    console.log(newValue.count)
  })

  return {
    state
  }
}
```

options api

[https://codepen.io/sdras/pen/69c0a34844f0775e3f78df3c432421ea](https://codepen.io/sdras/pen/69c0a34844f0775e3f78df3c432421ea)

composition api

[https://codepen.io/sdras/pen/b540be9253350508582c38ba1b20b317](https://codepen.io/sdras/pen/b540be9253350508582c38ba1b20b317)

## WatchEffect(new)

- Like watchers, with small differences. Executes the function immediately, and tracks **all t**he reactive state properties it used during the execution as dependencies (pretty neat)

```jsx
setup() {
  const state = reactive({
    count: 0
  })

  watchEffect(() => {
    console.log(state.count)
  })

  return {
    state
  }
}
```

[https://codepen.io/sdras/pen/201245ca475b4efeb4f63bdc79c23358](https://codepen.io/sdras/pen/201245ca475b4efeb4f63bdc79c23358)

## Props

- Just like you're used to using them, they are reactive, but passed into setup

```jsx
props: {
  count: {
    type: Number,
    required: true
  }
},
setup(props) {
  watchEffect(() => {
    console.log(props.count)
  })
}
```

## Context

- Passed as the second argument in setup
- Things like $emit, $attrs, etc would be accessed here

```jsx
// context is the second arg passed in
setup(props, context) {
  context.emit('eventName')
}

// can be destructed
setup(props, {emit}) {
  emit('eventName')
}
```

## Lifecycle Hooks

- Hooks are named the same, but prefixed with `on`, in camelCase (similar to React)

```jsx
setup() {
  const state = reactive({
    count: 0
  })

  onMounted(() => {
    console.log(state.count)
  })

  return {
    state
  }
}
```

# GREAT FOR REUSABLE LOGIC**SOME EXAMPLES:**

- getting dimensions of the viewport and component
  - extract the logic and not the template
- gathering specific mousemove events
- base elements of charts
- clipboards
- media queries
- dark mode

## EXAMPLE OF USING COMPOSITION API WITH OPTIONS API

[https://codesandbox.io/s/simple-options-api-importing-composition-api-yfhpv?from-embed](https://codesandbox.io/s/simple-options-api-importing-composition-api-yfhpv?from-embed)

- `/composables` folder - for composition api stuff

`/composables/useWindowWidth.js`

```jsx
import { ref, onMounted } from '@vue/composition-api'

export function useWindowWidth() {
  // same as data, width = ''
  const width = ref(0)

  onMounted(() => {
    width.value = window.innerWidth
  })

  return {
    width,
  }
}
```

`App.vue`

```jsx
<template>
  <div id="app">
    <h2>Options API</h2>
    <p>This is an example of the Options API</p>
    <p>{{ message }}</p>
    <h2>Composition API</h2>
    <p>We brought this in from the Composition API!</p>
    <p>{{ width }}</p>
    <button @click="reportWidth">Show Width in Alert Box</button>
    <p>{{ widthDoubled }}</p>
  </div>
</template>

<script>
// import it
import { useWindowWidth } from "@/composables/useWindowWidth.js";

export default {
  data() {
    return {
      message: "Hi from Options API!"
    };
  },

// set it up
  setup() {
    const { width } = useWindowWidth();

	// return it
    return {
      width
    };
  },

// now we can use the width in our component instance / options api
// its like data so it's still this.width
  computed: {
    widthDoubled() {
			// like here
      return this.width * 2;
    }
  },
  methods: {
    reportWidth() {

			// or here
      alert(this.width);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

##

# **SFC SUGAR 🍭** In Single File Components

# `<script setup>`

```jsx
<script setup>
  const state = reactive({
    count: 0
  })

  onMounted(() => {
    console.log(state.count)
  })

  return {
    state
  }
</script>
```

## cont.. with exercise!!

& custom directives
