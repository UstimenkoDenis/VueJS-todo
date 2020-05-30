<template>
    <ul class="grouplist">      
        <Group 
            v-for="(items, index) in groupData"
            v-bind:key="`${index}`"
            v-bind:item="items"
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
    }
}
</script>

<style>
    .grouplist {
        display:flex;
        padding: 0;
        margin: 0;
    }
</style>
