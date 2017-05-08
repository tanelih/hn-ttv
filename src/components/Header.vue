<template>
  <header class="header">
    <span class="header__big-title">HN</span>
    <span class="header__sub-title">Teksti-TV</span>
    <section class="header__banner">
      <a :href="url" target="_blank" rel="noopener noreferrer">
        {{ url }}
      </a>
    </section>
  </header>
</template>
<script>
  export default {
    data () {
      return {
        url: 'https://hn-ttv.firebaseapp.com'
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import "../constants";

  .header {
    flex: 0 1;

    margin:  0      $ttv-v-margin;
    padding: 0.4rem 0;

    color:      $ttv-foreground;
    background: $ttv-blue;

    &__big-title {
      padding-left: $ttv-v-margin;
      font-size:    4.0rem;
    }

    &__sub-title {
      font-size: 2.0rem;
    }

    &__banner {
      padding-left: $ttv-v-margin;
      font-size:    1.4rem;
      background:   $ttv-cyan;

      a {
        color:           $ttv-blue;
        text-decoration: none;
      }
    }
  }
</style>
