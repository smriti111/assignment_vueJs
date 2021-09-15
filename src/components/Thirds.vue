<template>
    <Table :tasks="tasks"/>
</template>

<script>
import Table from './Table.vue'

export default {
    components:{
        Table,
    },
    props:{
        tasks: Array
    }
}
</script>