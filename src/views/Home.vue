<template>
  <div class="home container">
    <Items @add-count="addCount" @subtr-count="subtrCount" :items="items" />
  </div>
</template>

<script>
// @ is an alias to /src
import Items from '@/components/Items.vue'

export default {
  name: 'Home',
  components: {
    Items
  },
  data() {
    return {
      items: []
    }
  },
  methods: {
    addCount(id) {
      this.items[id].count++
    },
    subtrCount(id) {
      this.items[id].count--
    }
  },
  created() {
    this.items = [
      {
        id: 0,
        text: 'An item',
        config: {},
        count: 2
      },
      {
        id: 1,
        text: 'Another item',
        config: {},
        count: 5
      },
      {
        id: 2,
        text: 'Different item',
        config: {},
        count: 73
      }
    ]
  }
}
</script>

<style scoped>
  .home {
    margin-top: 7em;
  }
</style>
