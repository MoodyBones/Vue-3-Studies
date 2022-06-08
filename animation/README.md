# Vue 3 Studies - Animation / Transitions

- 🚌&nbsp;&nbsp; Course on [Frontend Masters](https://frontendmasters.com/courses/vue-3/)
- 👩‍🏫&nbsp;&nbsp; Taught by [Sarah Drasner](https://twitter.com/sarah_edo)
- 📓&nbsp;&nbsp; Notes by [Mel Jones](https://twitter.com/_moodybones)
- 📎&nbsp;&nbsp; Link to [GitHub Starter Docs & Slides](https://github.com/sdras/intro-to-vue)

### [Slides](https://slides.com/sdrasner/intro-to-vue-3-5?token=YXhIwtpW#/1)

## Transitions vs. animation

- Surface API pieces
- Hooks to obsever things

CSS Transitions

- interpolate 2 states
- no loops

CSS Animations

- Have access Keyframes
- can have more 2 states
- but has more power
- can make loops

Vue Transition Component

- hooks into both CSS Transitions & CSS Animations

```js
<script type="text/x-template" id="childarea">
  <div>
    <h2>Here I am!</h2>
    <slot></slot>
  </div>
</script>
```

```js
<div id="app">
    <h3>Let's trigger this here modal!</h3>
    <button @click="toggleShow">
      <span v-if="isShowing">Hide child</span>
      <span v-else>Show child</span>
    </button>
    <app-child v-if="isShowing">
      <button @click="toggleShow">
        Close
      </button>
    </app-child>
</div>

const app = Vue.createApp({
  data() {
    return {
      isShowing: false
    }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    }
  },
})

app.component('app-child', {
  template: '#childarea'
})

app.mount('#app')
```

[Transition Demo - base without transition v3](https://codepen.io/sdras/pen/ef162928e468cfd1a7aeb4b9bd90e70f)

## But Humans need flow of state - no jerky changes

- Wrap the child component in a transition

```js
<transition name="fade">
  <app-child v-if="isShowing" class="modal">
    <button @click="toggleShow">
      Close
    </button>
  </app-child>
</transition>
```

![v-enter-active v-leave-active](/animation/v-enter-v-leave.png)

- Vue 2 had only enter and leave
- Vue 3 more explicit with enter-from enter-to / leave-from leave-to

## Reactivity / Hooks to observe things

- the moment you start hovering
- the time it takes to hover and what it's going to do in between that state
- and the second that its done

## Reusable for other Components

```css
.fade-enter-active {
  transition: opacity 0.25s ease-out; /*  any time the opacity is changing, i want you to change it this way */
}

.fade-leave-active {
  transition: opacity 0.2s ease-in;
}

.fade-enter-from,
.fade-leave-to {
  /* start state */
  opacity: 0;
}
```

This is unnecessary, as it's default - DOM elements have an opacity of 1 by default:

```css
.fade-enter-to,
.fade-leave-from {
  opacity: 1;
}
```

### Realistic Animation tip - enter-active should be ease-out & leave-active should be ease-in

[Transition Demo- simple transition, v3](https://codepen.io/sdras/pen/7bab1d8163c2ab2494c815633add1d83)
