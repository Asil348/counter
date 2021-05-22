<template>
    <div :key="item.id" v-for="item in items">
        <Item @add-count="$emit('add-count', item.id)" @subtr-count="$emit('subtr-count', item.id)" :item="item" />
    </div>
</template>

<script>
import Item from './Item'

export default {
    name: 'Items',
    props: {
        items: Array
    },
    components: {
        Item
    },
    emits: ['add-count', 'subtr-count']
}
</script>