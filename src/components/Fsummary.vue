<template>
  <div class="base">
    <div class="summary-row">
      <span v-for="namePrice in this.pending.baseDrinks">
        <fdrink :drinkname="namePrice.name" :cost:"namePrice.price"></fdrink>
      </span>
    </div>
  </div>
</template>

<script>
// import axios from 'axios'
import Fmodifier from './Fmodifier.vue'
import Fdrink from './Fdrink.vue'
export default {
  name: 'fsummary',
  props: ['pending'],
  components: {
    Fdrink,
    Fmodifier
  },
  data () {
    return {
      baseDrinkCosts: [],
      errors: []
    }
  },

  methods: {
  }
}

</script>

<style scoped lang="sass">

.base
  width: 400px

.drinks-row
  display: flex
  height: 200px
  overflow: hidden
</style>
