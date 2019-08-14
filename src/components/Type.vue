<template>
  <div class="ml-1" :class="`type-${type.type.name}`">
    <span>{{ type.type.name | capitalize }}</span>
  </div>
</template>

<script>
export default {
  name: 'Type',
  props: {
    type: Object
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
