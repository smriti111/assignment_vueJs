<template>
    <Table :tasks="tasks"/>
</template>

<script>
import Table from './Table.vue'
export default {
    props:{
        tasks: Array
    },
    components:{
        Table
    }
}
</script>