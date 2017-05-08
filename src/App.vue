<template>
  <section class="app">
    <ttv-header />
    <ttv-error v-if="error" :error="error" />
    <ul class="story-list">
      <ttv-story :key="story.id" :story="story" v-for="story in stories" />
    </ul>
    <ttv-footer />
  </section>
</template>

<script>
  import 'isomorphic-fetch'

  import TTVStory  from './components/Story.vue'
  import TTVError  from './components/Error.vue'
  import TTVHeader from './components/Header.vue'
  import TTVFooter from './components/Footer.vue'

  const BACKEND_URL = 'https://hacker-news.firebaseio.com/v0'
  const REFRESH_INTERVAL_MIN = 5 * 60 * 1000
  const NUM_STORIES = 5

  export default {
    data () {
      return {
        error:   null,
        stories: [],
      }
    },
    components: {
      'ttv-story':  TTVStory,
      'ttv-error':  TTVError,
      'ttv-header': TTVHeader,
      'ttv-footer': TTVFooter,
    },
    methods: {
      poll () {
        this.fetchStories()
          .then(ids => ids.slice(0, NUM_STORIES))
          .then(ids => Promise.all(ids.map(this.fetchStory)))
          .then(stories => (this.stories = stories))
          .catch(err => (this.error = err))
      },
      fetchStory (id) {
        return fetch(`${BACKEND_URL}/item/${id}.json`)
          .then(response => response.json())
      },
      fetchStories () {
        return fetch(`${BACKEND_URL}/topstories.json`)
          .then(response => response.json())
      },
    },
    mounted () {
      this.poll()
      setInterval(this.poll, REFRESH_INTERVAL_MIN)
    }
  }
</script>
<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=VT323');
  @import "./constants";

  body {
    height: 100vh;

    margin:     0;
    padding:    0;

    display:     flex;
    align-items: center;

    background: $ttv-background;
  }
</style>
<style lang="scss" scoped>
  @import "./constants";

  .app {
    display:        flex;
    flex-direction: column;

    margin: 0 auto;

    width:      100vw;
    height:     100vh;
    max-width:  $ttv-width;
    max-height: $ttv-height;

    background:  black;
    font-family: VT323, monospace;

    .story-list {
      flex: 1 1 auto;

      margin:  0 $ttv-v-margin;
      padding: 0.8rem 0;

      list-style: none;
    }
  }
</style>
