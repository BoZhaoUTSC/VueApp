<template>
  <div>
    <nav>
        <ul>
            <a href="#" @click="changeTab('new-selection')"><li>New Selection</li></a>
            <a href="#" @click="changeTab('selection-summary')"><li>Selection Summary</li></a>
        </ul>
    </nav>

      <div v-show="currentTab === 'new-selection'">
        <fdrinks drinks="drinks"></fdrinks>
      </div>
      <div v-show="currentTab === 'selection-summary'">
        showing selection summary
      </div>
  </div>
</template>

<script>
import Fdrinks from './Fdrinks.vue'
import axios from 'axios'
export default {
  name: 'root',
  components: {
    Fdrinks
  },
  data () {
    return {
      currentTab: 'new-selection',
      drinks: [],
      errors: []
    }
  },
  created () {
    axios.get('http://localhost:3000/drinks')
    .then(res => {
      this.drinks = res.data
    })
    .catch(error => {
      this.errors.push(error)
    })
  },
  methods: {
    changeTab: function (tabName) {
      this.currentTab = tabName
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
