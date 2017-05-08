<template>
  <div class="error">{{ error.message }}</div>
</template>
<script>
  export default {
    props: [
      'error'
    ]
  }
</script>
