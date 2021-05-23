<template>
  <div class="home container">
      <AddItem :items="items" @add-item="addItem"/>
    <Items @add-count="addCount" @subtr-count="subtrCount" :items="items" />
  </div>
</template>

<script>
// @ is an alias to /src
import Items from '@/components/Items.vue'
import AddItem from '@/components/AddItem.vue'

export default {
  name: 'Home',
  components: {
    Items,
    AddItem
  },
  data() {
    return {
      items: []
    }
  },
  methods: {
    addCount(id) {
      this.items[id].count += this.items[id].config.increment;
    },

    subtrCount(id) {
      this.items[id].count -= this.items[id].config.increment;
    },

    addItem(newItem) {
      this.items = [...this.items, newItem]
    }
  },
  created() {
    this.items = [
      {
        id: 0,
        text: 'An item',
        config: {
          increment: 1,
          reminder: false
        },
        count: 2,
      },
      {
        id: 1,
        text: 'Another item',
        config: {
          increment: 2,
          reminder: false
        },
        count: 5
      },
      {
        id: 2,
        text: 'Different item',
        config: {
          increment: 3,
          reminder: true
        },
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
