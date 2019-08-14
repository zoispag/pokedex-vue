<template>
  <div id="app">
    <div class="pokelist">
      <Pokemon v-for="i in maxCount" :key="`Pokemon${i}`" :poke-id="i" />
    </div>
    <div class="flex mx-auto">
      <button
        class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
        @click="loadMore"
      >Load more {{ maxCount }}</button>
    </div>
  </div>
</template>

<script>
import Pokemon from '@/components/Pokemon.vue'

export default {
  name: 'app',
  components: {
    Pokemon
  },
  data () {
    return {
      maxCount: 50
    }
  },
  methods: {
    loadMore () {
      this.maxCount += 50
    }
  }
}
</script>

<style lang="scss">
.pokelist {
  @apply flex mx-auto max-w-full w-screen flex-wrap;
}
</style>
