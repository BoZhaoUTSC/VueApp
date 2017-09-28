<template>
  <div>
    <nav>
        <ul>
            <a href="#" @click="changeTab('new-selection')"><li>New Selection</li></a>
            <a href="#" @click="changeTab('selection-summary')"><li>Selection Summary</li></a>
        </ul>
    </nav>

      <div v-show="currentTab === 'new-selection'">
        <fsizes></fsizes>
        <fdrinks></fdrinks>
        <fmodifiers></fmodifiers>
        <fcomfirm :result="this.result" @addNew="verifyPendingDrink"></fcomfirm>
      </div>
      <div v-show="currentTab === 'selection-summary'">
        showing selection summary
      </div>
  </div>
</template>

<script>
import Fsizes from './Fsizes.vue'
import Fdrinks from './Fdrinks.vue'
import Fmodifiers from './Fmodifiers.vue'
import Fcomfirm from './Fconfirm.vue'
export default {
  name: 'root',
  components: {
    Fdrinks,
    Fsizes,
    Fmodifiers,
    Fcomfirm
  },
  data () {
    return {
      currentTab: 'new-selection',
      pending: {
        size: '',
        baseDrinks: [],
        modifiers: [],
        quantity: []
      },
      errors: [],
      result: ''
    }
  },
  methods: {
    changeTab: function (tabName) {
      this.currentTab = tabName
    },

    verifyPendingDrink: function () {
      if (this.pending.size === '') {
        this.result = 'Select drink size'
      } else if (this.pending.baseDrinks.length === 0) {
        this.result = 'Select at least one base drink'
      } else if (!this.pending.quantity === 0) {
        this.result = 'Quantity cannot be 0'
      } else {
        this.result = 'Added, quantity is ' + this.pending + '.'
      }
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


@media screen and (max-width: 1080px)
    nav ul li
        width: 100%
        box-sizing: border-box
</style>
