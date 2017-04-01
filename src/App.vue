<template>
  <section class="app">
    <header class="header">
      <span class="header__big-title">HN</span>
      <span class="header__sub-title">Teksti-TV</span>
      <section class="header__banner">
        https://hn-ttv.firebaseapp.io
      </section>
    </header>
    <div v-if="error" class="error">
      {{ error }}
    </div>
    <ul class="stories">
      <li v-for="story in stories" class="stories__item">
        <span class="stories__item__link">
          {{ story.id }}
        </span>
        <span class="stories__item__title">
          {{ story.title }}
        </span>
      </li>
    </ul>
    <footer class="footer">
      TODO
    </footer>
  </section>
</template>

<script>
  import 'isomorphic-fetch'

  const url = 'https://hacker-news.firebaseio.com/v0'

  export default {
    data () {
      return {
        error:   null,
        stories: [],
      }
    },
    methods: {
      poll () {
        this.fetchStories()
          .then(ids => ids.slice(0, 5))
          .then(ids => Promise.all(ids.map(this.fetchStory)))
          .then(stories => (this.stories = stories))
          .catch(err => (this.error = err))
      },
      fetchStory (id) {
        return fetch(`${url}/item/${id}.json`)
          .then(response => response.json())
      },
      fetchStories () {
        return fetch(`${url}/topstories.json`)
          .then(response => response.json())
      },
    },
    mounted () {
      this.poll()
      setInterval(this.poll, 5 * 60 * 1000)
    }
  }
</script>

<style lang="scss" scoped>
  @import url('https://fonts.googleapis.com/css?family=VT323');

  .app {
    background:  black;
    font-family: 'VT323', monospace;

    & .header {
      color:      white;
      background: blue;

      padding: 0.4rem 0;

      &__big-title {
        font-size:    4.0rem;
        padding-left: 2.0rem;
      }

      &__sub-title {
        font-size: 2.0rem;
      }

      &__banner {
        color:        blue;
        background:   cyan;
        padding-left: 2.0rem;
        font-size:    1.4rem;
      }
    }

    & .footer {
      color:      white;
      background: blue;
    }
  }

  .stories {
    margin:     0;
    padding:    0.8rem 2.0rem;
    list-style: none;

    &__item {
      display: flex;

      color: white;
      font-size: 2.0rem;

      &__link {
        color:        green;
        margin-right: 0.8rem;
      }

      &__title { color: white; }
    }
  }

  .app {
    display:        flex;
    flex-direction: column;

    width:  100vw;
    height: 100vh;

    .header  { flex: 0 1; }
    .footer  { flex: 0 1; }
    .stories { flex: 1 0 auto; }
  }

</style>

