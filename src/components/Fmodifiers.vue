<template>
  <div class="base">
    <h1>
        Modifiers
    </h1>
    <div class="modifierss-row">
        <div v-for="modifier in this.modifiers">
          <!-- only render that modifiers that are available -->
          <div v-if="modifier.isAvailable">
            <fmodifier :modifiername="modifier.name" :cost="modifier.cost"></fmodifier>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
import Fmodifier from './Fmodifier.vue'
import axios from 'axios'
export default {
  name: 'fmodifiers',
  components: {
    Fmodifier
  },

  data () {
    return {
      modifiers: []
    }
  },

  created () {
    // get all the drinks
    axios.get('http://localhost:3000/modifiers')
    .then(res => {
      this.modifiers = res.data
    })
    .catch(error => {
      this.errors.push(error)
    })
  }
}

</script>

<style scoped lang="sass">

.modifiers-row
    display: flex
    height: 200px
    overflow: hidden
</style>
