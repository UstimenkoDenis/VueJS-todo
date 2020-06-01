<template>
    <ul class="cardlist">        
        <Card 
            v-for="card in cardsData"
            v-bind:key="card.id"
            v-bind:card="card"
            v-on:onDelete="deleteCard"
        />
    </ul>    
</template>

<script>
import Card from '../Card/Card'
export default {
    components: {
        Card
    },
    props: ['cardsData'], 
    data() {
        return {
                      
        }
    },
    methods: {
        deleteCard(id) {
           this.$emit('onDelete', id)
            
        }
    }
}
</script>

<style>
    .cardlist {
        display:flex;
        padding: 0;
        margin: 0;
        width: 100%;
        overflow-x: scroll;  
    }
    .cardlist::-webkit-scrollbar {height:0px;}
</style>
