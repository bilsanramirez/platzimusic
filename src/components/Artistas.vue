<template lang="pug">
li
  h2: a(v-bind:href="artista.url", target="_blank") {{ artista.name }}
  img(v-bind:src="artista.image[2]['#text']")
</template>

<script>

export default {
  name: 'artista',
  props: ['artista']
}
</script>

<style lang="stylus" scoped>
li
  display block
  margin 10px 0
</style>
