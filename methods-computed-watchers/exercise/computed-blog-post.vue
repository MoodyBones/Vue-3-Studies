<template>
  <div id="app" class="bg-gray-100 text-gray-700 flex flex-col items-center">
    <section class="px-4 md:px-0 md:w-2/3 my-16 space-y-6 max-w-screen-sm">
      <form class="py-10 space-y-4" @submit.prevent="addPost">
        <h2 class="text-gray-800 tracking-tight text-3xl font-bold mb-6">
          {{ headingLabel }} ✨
        </h2>
        <div class="flex justify-between space-x-2">
          <input
            class="w-1/2 p-2 rounded-sm focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-50"
            type="text"
            :placeholder="titleLabel"
            v-model="newTitle"
            required
          />
          <input
            class="w-1/2 p-2 rounded-sm focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-50"
            type="text"
            :placeholder="authorLabel"
            v-model="newAuthor"
            required
          />
        </div>
        <input
          class="w-full p-2 rounded-sm focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-50"
          :placeholder="urlLabel"
          v-model="newURL"
          required
        />
        <!--           type="url" -->
        <select
          class="w-full p-2 rounded-sm focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-50"
          v-model="newCategory"
          required
        >
          <optgroup :label="categoriesPlaceholder" />
          <option
            v-for="(value, index) in categoriesList"
            :key="`${index}-${value}`"
          >
            {{ value }}
          </option>
        </select>
        <button
          :class="newTitle ? 'bg-opacity-100' : 'bg-opacity-25'"
          class="bg-indigo-600 tracking-wide hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-700 focus:ring-opacity-50 py-2 px-3 rounded w-full text-gray-100 uppercase"
          type="submit"
        >
          {{ buttonLabel }}
        </button>
      </form>
      <div class="border-t-2 pt-20">
        <div class="flex flex-col items-end space-y-2">
          <label for="sort" class="uppercase tracking-wide font-bold text-sm">
            SORT BY
          </label>
          <select
            name="sort"
            v-model="selectedCategory"
            class="px-3 py-2 border rounded-lg hover:opacity-100 uppercase tracking-wide"
          >
            <option
              v-for="(value, index) in categoriesList"
              :key="`${index}-${value}`"
            >
              {{ value }}
            </option>
          </select>
        </div>
      </div>
      <div
        v-for="(value, index) in filteredCategories"
        :key="`${index}-${value}`"
      >
        <article class="bg-white px-6 py-10 rounded-lg border hover:shadow">
          <a :href="value.url" target="_blank" rel="noreferrer noopener">
            <div class="flex flex-col space-y-6">
              <h3 class="text-xl font-bold">{{ value.title }}</h3>
              <div class="flex flex-nowrap justify-between items-end">
                <div
                  class="text-indigo-700 font-bold uppercase opacity-75 text-sm tracking-wide pb-2 border-b-2 border-transparent hover:border-indigo-600 hover:opacity-100 transition"
                >
                  by {{ value.author }}
                </div>
                <div
                  class="uppercase tracking-wide border-2 text-gray-500 border-gray-400 rounded-lg px-3 py-2 text-center text-sm font-bold hover:bg-gray-400 hover:text-white transition"
                >
                  {{ value.category }}
                </div>
              </div>
            </div>
          </a>
        </article>
      </div>
    </section>
    <footer class="text-sm pb-10 uppercase tracking-wider">
      <a href="https://meljones.netlify.app/">Made by Moody ✌️ 🌞 🤚</a>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      headingLabel: 'Add a new post',
      titleLabel: 'Title',
      authorLabel: "Author's Name",
      urlLabel: 'URL',
      categoriesPlaceholder: 'Add a label',
      categoriesList: ['Cognition', 'Collection', 'Connection', 'Creation'],
      buttonLabel: 'Add a new blog post',
      newTitle: '',
      newAuthor: '',
      newURL: '',
      newCategory: '',
      selectedCategory: '',
      post: [
        {
          title: 'A theory of AI and remote co-creativity',
          author: 'LAV R. VARSHNEY',
          category: 'Cognition',
          url:
            'https://increment.com/remote/artificial-intelligence-remote-creative-collaboration/',
        },
        {
          title: 'Textual maps and the future of text',
          author: 'Anne-Laure Le Cunff',
          category: 'Collection',
          url: 'https://nesslabs.com/textual-maps-and-the-future-of-text',
        },
        {
          title: 'How to Chain Trip?',
          author: 'Claire L. Evans',
          category: 'Creation',
          url: 'https://youtu.be/ebZIO0tG8G0',
        },
      ],
    }
  },
  methods: {
    addPost() {
      let addedPost = {
        title: this.newTitle,
        author: this.newAuthor,
        url: this.newURL,
        category: this.newCategory,
      }

      this.post.push(addedPost)
      this.newTitle = ''
      this.newAuthor = ''
      this.newURL = ''
      this.newCategory = ''
    },
  },
  computed: {
    filteredCategories() {
      let filter = new RegExp(this.selectedCategory, 'i')
      return this.post.filter((el) => el.category.match(filter))
    },
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;700&display=swap');

body {
  font-family: 'Noto Sans', sans-serif;
}

#app {
  height: auto;
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-content: center;
}
</style>
