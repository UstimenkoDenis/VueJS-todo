<template>
    <ul 
        class="cardlist"
        v-on:dragover="dragOver"       
        v-on:drop="dragDrop"
    >        
        <Card 
            v-for="card in filteredCards(this.cardsData, this.term)"
            v-bind:key="card.id"
            v-bind:card="card"
            v-on:onDelete="deleteCard"
            @onDragId = "onDragId"
            @dragCardOrItem = "onDragCard"
        />
    </ul>    
</template>

<script>
import Card from '../Card/Card'
export default {
    components: {
        Card
    },
    props: ['cardsData', 'term', 'filter', 'dragId'], 
    data() {
        return {
                      
        }
    },
    methods: {
        dragOver(evt){
            evt.preventDefault()
        },
        dragDrop() {
            this.addItemInList(this.dragId)
        },
        addItemInList(dragId) {
           return this.$emit('addItemInList', dragId)
        },
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
            
        },
        onDragId(id) {
            return this.$emit('onDragId', id)
        },
        onDragCard() {
            return this.$emit('dragCardOrItem', 'card')
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
        min-height: 100%;
        overflow-x: scroll;  
    }
    .cardlist::-webkit-scrollbar {height:0px;}
</style>
