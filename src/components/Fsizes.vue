<template>
  <div class="base">
    <h1>
        Sizes
    </h1>
    <div class="sizes-row">
        <button class="small">Small</button>
        <button class="medium">Medium</button>
        <button class="large">Large</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'fsizes',

  data () {
    return {
      drinks: []
    }
  }
}

</script>

<style scoped lang="sass">
$background-color: #00BFFF

.sizes-row
    display: flex
    height: 200px
    overflow: hidden
    height: 100px

button
    margin: 10px
    width: 15%
    color: white
    padding: 15px 32px
    text-align: center
    text-decoration: none
    display: inline-block
    font-size: 16px

.small
    @extend button
    background-color: $background-color

.medium
    @extend button
    background-color: $background-color - 40

.large
    @extend button
    background-color: $background-color - 80

</style>
