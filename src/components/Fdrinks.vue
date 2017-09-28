<template>
  <div class="base">
    <h1>
        Base Drinks
    </h1>
    <div class="drinks-row">
      <div v-for="drink in this.drinks">
        <!-- only render that drinks that are available -->
        <div v-if="drink.isAvailable">
          <fdrink :drinkname="drink.name" :cost="drink.cost" @drinkSelect="udpateSelectedDrinks($event)"></fdrink>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Fdrink from './Fdrink.vue'
import axios from 'axios'
export default {
  name: 'fdrinks',
  components: {
    Fdrink
  },

  data () {
    return {
      drinks: [], // a list of all the drinks
      selectedDrinks: [], // a list of all the drinks selected {name, cost}
      errors: []
    }
  },

  created () {
    // get all the drinks
    axios.get('http://localhost:3000/drinks')
      .then(res => {
        this.drinks = res.data
      })
      .catch(error => {
        this.errors.push(error)
      })
  },

  methods: {
    udpateSelectedDrinks: function (namePrice) {
      console.log(namePrice)
      var i = this.selectedDrinks.indexOf(namePrice)
      // remove from selected this drink is selected
      if (i >= 0) {
        this.selectedDrinks.splice(i, 1)
      } else { // add to selected if not selected
        this.selectedDrinks.push(namePrice)
      }
      this.$emit('selectedDrinks', this.selectedDrinks)
    }
  }
}

</script>

<style scoped lang="sass">

.drinks-row
    display: flex
    height: 200px
    overflow: hidden
</style>
