<template>
  <div>
    <nav>
        <ul>
            <a href="#" @click="changeTab('new-selection')"><li>New Selection</li></a>
            <a href="#" @click="changeTab('selection-summary')"><li>Selection Summary</li></a>
        </ul>
    </nav>

      <div v-show="currentTab === 'new-selection'">
        showing new selection
      </div>
      <div v-show="currentTab === 'selection-summary'">
        showing selection summary
      </div>
  </div>
</template>

<script>
export default {
  name: 'root',
  data () {
    return {
      currentTab: 'new-selection'
    }
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
