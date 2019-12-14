<template>
  <div class="tower-item">
    {{ params.title }} {{ params.id }}
  </div>
</template>

<script>
export default {
  name: 'TowerItem',
  props: {
    params: {
      type: Object
    },
  },
  data () {
    return {} 
  }
}
</script>

<style scoped>

</style>
