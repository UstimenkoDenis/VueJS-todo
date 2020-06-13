<template>
    <li 
        class="card"
        draggable="true"
        v-on:dragstart="dragStart"
        v-on:dragend="dragEnd"
        v-bind:class="{cardopened: cardtoggle, hide: cardHide}"        
        >
        <div class="card__header flex-between">
            <div 
                class="card__title flex-center"
                v-bind:class="{done: card.completed}"
            >
                {{card.title | uppercase}}
            </div>
            <div class="card__controls">
                <input 
                    class="checkbox"
                    type="checkbox"
                    v-on:change="card.completed = !card.completed" 
                >
                <div   
                    class="card-open-button" 
                    v-on:click="cardtoggle=!cardtoggle"
                ></div>  
                <div 
                    class="delete-button"
                    v-on:click="onDelete(card.id)"
                ></div>  
            </div>                     
        </div>
        <div
            class="card__body"            
        >
            {{card.description}}
        </div>
    </li>
</template> 

<script>
export default {
    props: {
        card:{
            type: Object,
            required: true
        }
    },
    data() {
        return {
            cardtoggle: false,
            cardHide: false
        }
    },
    methods: {
        onDelete(id) {
            return this.$emit('onDelete', id)
        },
        dragStart() {
            setTimeout(()=>{
                this.cardHide = true               
                return (
                    this.$emit('onDragId', this.card.id),
                    this.$emit('dragCardOrItem', 'card')
                )
            },0)        
        },
        dragEnd() {
            this.cardHide = false                    
        }
    },
    filters: {
        uppercase(value) {           
            return value.toUpperCase()
        }
    }
}
</script>


<style>

    .card {
        display: flex;
        flex-direction: column;      
        height: 130px;      
        background:#f0f4c3 ;       
        margin: 1.2rem 0.6rem;
        border: 0.1rem solid #f0f4c3;
        border-radius: 5px;
      
    }
    @media (max-width: 768px) {
      .card {
         /* min-width: 400px; */
         height: 300px;
      }      
    }
        .hide {
            display: none;
        }
        .cardopened {
            height: 100%;         
        }
        .card:first-child {
            margin: 1.2rem 0.6rem 1.2rem 1.2rem;
        }
        .card__header {
            width: 100%;           
            background: #fff;
            color: #90caf9;           
        } 
        
            .card__title {                 
               padding: 0 0.4rem;                                                        
            }
            @media (max-width: 768px) {
                .card__title {
                    padding: 5px;
                }      
            }  
            .card__controls {
                display: flex;
                justify-content: center;
                align-items: center;
                padding: 0.1rem 0.2rem;
            }
            .checkbox {
                width: 20px;
                height: 20px;
                margin: 0 0.4rem 0 0.6rem;
            }
            .card-open-button {
                    position: relative;
                    left: 0;
                    top: 0;
                    width: 20px;
                    height:20px;
                    margin-right: 0.2rem;
                    background: #c8e6c9; 
                    border-radius: 50%;
            }
                .card-open-button:hover {
                    cursor: pointer;
                    box-shadow: 0 0 5px rgba(200, 230, 201, 0.568);
                    background: rgba(200, 230, 201, 0.637);
                }
                .card-open-button:active {
                    top: 2px;
                    box-shadow: 0 0 0;
                }
          
        .card__body {
            flex-grow: 1;
            padding: 0.8rem;
            color: rgba(0, 0, 0, 0.61);
            overflow: hidden;
        }        
</style>