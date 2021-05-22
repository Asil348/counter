<template>
  <div class="input-group item">
    <span class="input-group-text"><strong>{{ item.count }}</strong></span>
    <button @click="$emit('add-count', item.id)" class="btn btn-outline-success" type="button"><i class="bi bi-plus-lg"></i></button>
    <input type="text" class="form-control" :value="item.text">
    <button @click="$emit('subtr-count', item.id)" class="btn btn-outline-danger" type="button"><i class="bi bi-dash-lg"></i></button>
    <Settings :item="sItem" />
  </div>
</template>

<script>
  import Settings from './Settings'

  export default {
    name: 'Item',
    props: {
      item: Object
    },
    data() {
      return {
        sItem: this.item
      }
    },
    components: {
      Settings
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .item {
    width: 75vw;
    margin: 3em auto;
  }
</style>