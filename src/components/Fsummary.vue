<template>
  <div class="base">
    <div class="summary-row">
      <span v-for="namePrice in pending.baseDrinks">
        <fdrink :drinkname="namePrice.name" :cost="namePrice.price"></fdrink>
      </span>
      <span class="right">
        <h1> {{ '$' + getTotal() }}</h1>
      </span>
    </div>
  </div>
</template>

<script>

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
      total: this.getTotal(),
      errors: []
    }
  },

  methods: {
    getTotal: function () {
      // var result = 0
      var baseDrinksPrice = this.pending.baseDrinks.map(namePrice => {
        return parseFloat(namePrice.price)
      }).reduce((a, b) => {
        return a + b
      }, 0)
      var modifiersPrice = this.pending.modifiers.map(namePriceQuantity => {
        return parseFloat(namePriceQuantity.price) * namePriceQuantity.quantity
      }).reduce((a, b) => {
        return a + b
      }, 0)
      var result = (baseDrinksPrice + modifiersPrice) * this.pending.quantity
      this.$emit('reportTotal', result)
      return result
    }
  }
}

</script>

<style scoped lang="sass">

.base
  width: 100%

.summary-row
  display: flex
  height: 200px
  overflow: hidden

.right
    position: absolute
    right: 0px
    width: 300px
    padding: 10px



</style>
