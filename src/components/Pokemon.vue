<template>
  <div class="pokemon" v-if="loaded">
    <div class="whitespace-no-wrap text-center">(#{{ pokemon.id }}) <span class="font-bold">{{ pokemon.name | capitalize }}</span></div>
    <div class="mx-auto w-full">
      <v-lazy-image
        class="w-full"
        :src="pokemon.sprites.front_default"
        :src-placeholder="require(`@/assets/pokeball.png`)"
      />
      </div>
    <div class="flex"><Type v-for="type in typesArray" :key="type.name" :type="type"></Type></div>
  </div>
</template>

<script>
import VLazyImage from 'v-lazy-image'
import Type from '@/components/Type.vue'

export default {
  name: 'Pokemon',
  components: {
    VLazyImage,
    Type
  },
  props: {
    pokeId: Number
  },
  data () {
    return {
      loaded: false,
      pokemon: null
    }
  },
  created () {
    const url = `https://pokeapi.co/api/v2/pokemon/${this.pokeId}`
    fetch(url)
      .then(response => response.json())
      .then(data => {
        if (this.pokeId === 1) console.log(data)

        this.pokemon = data
        this.loaded = true
      })
      .catch(err => console.error(err))
  },
  computed: {
    typesArray () {
      return this.pokemon.types.slice().sort((a, b) => (a.slot > b.slot) ? 1 : ((b.slot > a.slot) ? -1 : 0))
    }
  },
  filters: {
    capitalize (val) {
      if (!val) return ''
      val = val.toString()
      return val.charAt(0).toUpperCase() + val.slice(1)
    }
  }
}
</script>

<style scoped lang="scss">
.pokemon {
  @apply w-1/6 p-8;
}
</style>
