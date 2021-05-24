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
    async addCount(id) {

      const toIncr = await this.getItemIndexById(id)

      const req = await this.fetchItem(id)
      const incrd = req.count += req.config.increment

      const res = await fetch(`api/items/${id}`, {
        method: 'PATCH',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify({ count: incrd })
      });

      const data = await res.json()

      this.items[toIncr].count = data.count;
      
    },

    async subtrCount(id) {
      
      const toDecr = await this.getItemIndexById(id)

      const req = await this.fetchItem(id)
      const decrd = req.count -= req.config.increment

      const res = await fetch(`api/items/${id}`, {
        method: 'PATCH',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify({ count: decrd })
      });

      const data = await res.json()

      this.items[toDecr].count = data.count;
    },

    async addItem(newItem) {
      const res = await fetch('api/items', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(newItem)
      });

      const data = await res.json()

      this.items = [...this.items, data]
    },

    async fetchItems() {
      const res = await fetch('api/items');

      const data = await res.json();

      return data;
    },
    async fetchItem(id) {
      const res = await fetch(`api/items/${id}`);

      const data = await res.json();

      return data;
    },
    async getItemIndexById(id) {
      const fetchedItems = await this.fetchItems()

      for (var i = 0; i < await fetchedItems.length; i++) {
        if (id === await fetchedItems[i].id) {
          return i
        }
      }
    }
  },
  async created() {
    this.items = await this.fetchItems();
  }
}
</script>

<style scoped>
  .home {
    margin-top: 7em;
  }
</style>
