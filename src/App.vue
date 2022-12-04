<template> 
  <div>
    
    <PokemonVue />

  </div>
</template>

<script>
import PokemonVue from './components/pokemon.vue';

export default {
  components: {PokemonVue},
  data() {
    return {
      show: false
    }
  },
  methods: {
    toggle() {
      this.show = !this.show
    }
  }
}
</script>

<style scoped>



</style>