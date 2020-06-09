<template>
    <ul class="grouplist"
    >      
        <Group 
        
            v-for="(items, index) in filteredGroups(this.groupData, this.groupTerm)"
            v-bind:key="`${index}`"
            v-bind:items="items"
            v-bind:filterGroup="filterGroup"           
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
    props: ['groupData', 'filterGroup', 'groupTerm'], 
    data() {
        return { 
            
        }
    },
    methods: {
        
        filteredGroups(groupData, groupTerm) {
           if(this.filterGroup === "name") {
                if(groupTerm === 0) {
                    return groupData
                }
            return groupData.filter((group) => {
                return (group.title).toUpperCase().indexOf(groupTerm.toUpperCase()) > -1
            })
           }
           if(this.filterGroup === "done") {
            return groupData
           }           
            
        },
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
