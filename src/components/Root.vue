<template>
  <div>
    <nav>
        <ul>
            <a href="#" @click="changeTab('new-selection')">
              <li>New Selection</li>
            </a>
            <a href="#" @click="changeTab('selection-summary'); addToSummary()">
              <li>Selection Summary</li>
            </a>
        </ul>
    </nav>
      <!-- show all options for adding a new drink for current purchase -->
      <div v-show="currentTab === 'new-selection'">
        <fsizes @selectSize="updateSize($event)"></fsizes>
        <fdrinks @selectedDrinks="updateBaseDrink($event)"></fdrinks>
        <fmodifiers @changeModifiers="updateModifiers($event)"></fmodifiers>
        <fcomfirm :result="this.result" @addNew="verifyPendingDrink" @clearAll="clearAll"></fcomfirm>
      </div>

      <!-- show all added drinks for current purchase -->
      <div v-show="currentTab === 'selection-summary'">
        <h1>
            Selection Summary
        </h1>
        <div class="drinks in summary">
          <div class="one-drink-in-summary" v-for="pending in addedDrinks">
            <fsummary :pending="pending"></fsummary>
          </div>
        </div>
      </div>
  </div>
</template>

<script>

import Fsizes from './Fsizes.vue'
import Fdrinks from './Fdrinks.vue'
import Fmodifiers from './Fmodifiers.vue'
import Fcomfirm from './Fconfirm.vue'
import Fsummary from './Fsummary.vue'

export default {
  name: 'root',
  components: {
    Fdrinks,
    Fsizes,
    Fmodifiers,
    Fcomfirm,
    Fsummary
  },
  data () {
    return {
      currentTab: 'new-selection',
      pending: { // current selction
        size: '',
        baseDrinks: [],
        modifiers: [],
        quantity: 0,
        valid: false
      },
      errors: [],
      addedDrinks: [],
      isVerified: false,
      result: ''
    }
  },
  methods: {
    changeTab: function (tabName) {
      this.currentTab = tabName
    },

    verifyPendingDrink: function () {
      if (this.pending.size === '') {
        this.result = 'Select drink size.'
      } else if (this.pending.baseDrinks.length === 0) {
        this.result = 'Select at least one base drink.'
      } else if (!this.pending.quantity === 0) {
        this.result = 'Quantity cannot be 0.'
      } else {
        // report quantity
        this.pending.quantity += 1
        this.result = 'Added, quantity is ' + this.pending.quantity + '.'
        this.isVerified = true
      }
    },

    updateModifiers: function (namePriceQuantity) {
      this.pending.modifiers = [namePriceQuantity]
    },

    addToSummary: function () {
      if (this.isVerified) {
        this.addedDrinks.push(this.pending)
      }
      this.isVerified = false
    },

    updateSize: function (size) {
      this.pending.size = size
      this.pending.quantity = 0
    },

    updateBaseDrink: function (baseDrinks) {
      this.pending.baseDrinks = baseDrinks
      this.pending.quantity = 0
      this.addToSummary()
      this.clearAll()
    },

    clearAll: function () {
      this.result = ''
    }
  }
}

</script>

<style scoped lang="sass">
$background-color: #00BFFF

nav ul
  background-color: $background-color
  text-align: center
  overflow: hidden
  padding: 0
  margin: 0
  color: white

nav
  ul
    li
      display: inline-block
      padding: 20px
      width: 30%

nav
  ul
    li:hover
      background-color: $background-color + 40

a
  color: inherit
  font-size: 32px

.drinks-in-summary
  display: flex


@media screen and (max-width: 1080px)
  nav ul li
    width: 100%
    box-sizing: border-box



</style>
