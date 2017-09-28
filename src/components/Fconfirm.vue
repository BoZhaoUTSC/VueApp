<template>
  <div class="base">
    <h1>
        Confirm
    </h1>
    <div class="sizes-row">
      <button class="add" @click="addNew">Add</button>
      <button class="clear">Clear</button>
      <span>
        <h2>{{ result }}</h2>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'fconfirm',
  props: ['result'],
  data () {
    return {
    }
  },
  methods: {
    addNew: function () {
      this.$emit('addNew')
    }
  }
}

</script>

<style scoped lang="sass">
$background-color: #00BFFF

h2
  color: red

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
    background-color: $background-color

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
