<template>
    <div :key="item.id" v-for="item in items">
        <Item @add-count="$emit('add-count', item.id)" @subtr-count="$emit('subtr-count', item.id)"
            @update-item="updateItem" :item="item" />
    </div>
</template>

<script>
    import Item from './Item'

    export default {
        name: 'Items',
        props: {
            items: Array
        },
        methods: {
            updateItem(updItem) {
                this.$emit('update-item', updItem)
            }
        },
        components: {
            Item
        },
        emits: ['add-count', 'subtr-count', 'update-item']
    }
</script>