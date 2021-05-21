<template>
  <div class="input-group item" style="width: 75%; margin: 3em auto">
    <span class="input-group-text"><strong>{{ item.count }}</strong></span>
    <button @click="$emit('add-count', item.id)" class="btn btn-outline-success" type="button"><i class="bi bi-plus-lg"></i></button>
    <input type="text" class="form-control" :value="item.text">
    <button class="btn btn-outline-danger" type="button"><i class="bi bi-dash-lg"></i></button>
    <button class="btn btn-outline-white" type="button"><i class="bi bi-sliders"></i></button>
  </div>
</template>

<script>

  export default {
    name: 'Item',
    props: {
      item: Object
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>