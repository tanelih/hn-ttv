<template>
  <footer class="footer">
    <section class="footer__top">
      Source at
    </section>
    <section class="footer__bottom">
      <a :href="url" target="_blank" rel="noopener noreferrer">
        {{ url }}
      </a>
    </section>
  </footer>
</template>
<script>
  export default {
    data () {
      return {
        url: 'https://github.com/tanelih/hn-ttv'
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import "../constants";

  .footer {
    flex:   0 1;
    margin: 0 2.0rem;

    color: $ttv-foreground;

    &__top {
      padding:    0.8rem $ttv-v-margin;
      font-size:  1.4rem;
      color:      $ttv-blue;
      background: $ttv-green;
    }

    &__bottom {
      padding:    0.8rem $ttv-v-margin;
      font-size:  1.4rem;
      background: $ttv-blue;

      a {
        color:           $ttv-foreground;
        text-decoration: none;
      }
    }
  }
</style>
