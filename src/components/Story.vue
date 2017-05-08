<template>
  <li class="story">
    <span class="story__link">
      <a :href="url" target="_blank" rel="noopener noreferrer">
        {{ story.id }}
      </a>
    </span>
    <span class="story__title">
      {{ story.title }}
    </span>
  </li>
</template>
<script>
  export default {
    props: [
      'story'
    ],
    computed: {
      url: c => `https://news.ycombinator.com/item?id=${c.story.id}`
    }
  }
</script>
<style lang="scss" scoped>
  @import "../constants";

  .story {
    display: flex;

    color:     $ttv-foreground;
    font-size: 2.0rem;

    &__link {
      margin-right: 1.2rem;

      a {
        color:           inherit;
        text-decoration: none;
      }
    }

    &:nth-child(2) {
      color:      $ttv-cyan;
      transform:  scaleY(0.70);
      margin-top: -0.25rem;
    }
  }
</style>
