<template>
    <div class="base" @click="toggleIsSelected()" :class="{ selected: isSelected }">
        <div class='img-div'>
            <img :src='imgSource'>
        </div>
        <div>
            {{ drinkname }}
        </div>
        <div>
            {{ "$" + cost }}
        </div>
    </div>
</template>

<script>
export default {
  name: 'fdrink',
  props: ['drinkname', 'cost'],
  data () {
    return {
      isSelected: false,
      imgSource: require('../assets/' + this.drinkname + '.jpg')
    }
  },
  methods: {
    toggleIsSelected: function () {
      this.isSelected = !this.isSelected
      var namePrice = {name: this.drinkname, price: this.cost}
      this.$emit('drinkSelect', namePrice)
    }
  }
}

</script>

<style scoped lang="sass">
$border-active: solid
$border-color: #00BFFF
$border-color-selected: $border-color - 40

.base
  width: 200px
  display: block
  margin: 20px
  height: 80%
  padding: 0
  border-color: white
  border-style: solid
  overflow: hidden
  cursor: pointer

.img-div
  width: 90%
  max-height: 100px
  overflow: hidden
  display: block
  box-shadow: 10
  border-bottom-style: ridge

.base
  div
    padding: 0

.selected
  border-style: $border-active
  border-color: $border-color-selected

.base:hover
  border-style: dotted
  border-color: $border-color

.base:active
  border-style: $border-active

</style>
