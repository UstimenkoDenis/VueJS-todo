<template>
    <ul class="grouplist">      
        <Group 
            v-for="(items, index) in groupData"
            v-bind:key="`${index}`"
            v-bind:items="items"
            @onDelGroup="deleteGroup"
            @onDelItem="deleteItem"
        />
    </ul>    
</template>

<script>
import Group from '../Group/Group'
export default {
   
    components: {
        Group
    },
    props: ['groupData'], 
    data() {
        return { 
            
        }
    },
    methods: {
        deleteGroup(id) {
            this.$emit('onDelGroup', id)           
        },
        deleteItem(id, idGroup) {
            this.$emit('onDelItem', id, idGroup)
        }
    }   
}
</script>

<style>
    .grouplist {
        display: flex;
        padding: 0;
        margin: 0;
        overflow-x: scroll; 
    }
    .grouplist::-webkit-scrollbar {height:0px;}
</style>
