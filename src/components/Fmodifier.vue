<template>
    <div class="base"  :class="{ selected: namePriceQuantity.quantity > 0 }">
      <div class="middle">
        <div class="info" @click="increaseCount()">
            {{ modifiername  + " $" + cost + " X " + namePriceQuantity.quantity }}
        </div>
        <div class="less" @click="decreaseCount()">
            {{ "less" }}
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'fmodifier',
  props: ['modifiername', 'cost'],
  data () {
    return {
      namePriceQuantity: {
        quantity: 0,
        price: this.cost,
        name: this.modifiername
      }
    }
  },
  methods: {
    increaseCount: function () {
      this.namePriceQuantity.quantity += 1
      this.$emit('changeModifier', this.namePriceQuantity)
    },
    decreaseCount: function () {
      if (this.namePriceQuantity.quantity > 0) {
        this.namePriceQuantity.quantity -= 1
        this.$emit('changeModifier', this.namePriceQuantity)
      }
    }
  }
}

</script>

<style scoped lang="sass">
$border-active: solid
$border-color: #00BFFF
$border-color-selected: $border-color - 40
$background-color: #00BFFF

.img-div
  width: 90%
  max-height: 100px
  overflow: hidden
  display: block
  box-shadow: 10
  border-bottom-style: ridge

.base
  margin: 5px
  width: 30%
  height: 80%
  padding: 0
  border-color: white
  border-style: solid
  overflow: hidden
  cursor: pointer
  display: inline-block

.middle
  padding: 0
  margin: 10px
  margin-left: auto
  margin-right: auto
  text-align: center
  display: flex


.selected
  border-style: $border-active
  border-color: $border-color-selected

.base:hover
  border-style: dotted
  border-color: $border-color

.base:active
  border-style: $border-active

.quantity-button
  background-color: $background-color
  margin: 10px
  color: white
  padding: 15px 32px
  text-align: center
  text-decoration: none
  display: inline-block
  font-size: 16px

.info
  @extend .quantity-button
  width: 80%


.less
  @extend .quantity-button
  width: 15%


</style>
