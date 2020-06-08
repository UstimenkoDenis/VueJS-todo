<template>
    <ul class="cardlist">        
        <Card 
            v-for="card in filteredCards(this.cardsData, this.term)"
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
    props: ['cardsData', 'term', 'filter'], 
    data() {
        return {
                      
        }
    },
    methods: {
        filteredCards(cardsData, term) {
            if(this.filter === 'done') {
                return cardsData.filter(card=>card.completed)
            }
                             
            if(this.filter === 'name') {            
                if(term.length === 0) {
                    return cardsData
                } else {
                        return cardsData.filter((card)=>{
                        return (card.title).toUpperCase().indexOf(term.toUpperCase()) > -1
                    })
                }
               
            }        
            
        },
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
