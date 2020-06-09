<template>
    <li class="group"
        v-bind:class="{hovered: hovered}"
    >
        <div class="group__header">
            <div class="group__title flex-center">
                {{items.title | uppercase}}
            </div>
            <div class="group__controls flex-center">               
                <div 
                    class="delete-button"
                    v-on:click="$emit('onDelGroup', items.id)"
                ></div>  
            </div>                     
        </div>
        <div class="group__body">
           <ul 
            class="group__list"
            v-on:dragover="dragOver"
            v-on:dragenter="dragEnter"
            v-on:dragleave="dragLeave"
            v-on:drop="dragDrop"
            
           >             
               <GroupItem
                    v-for="item in filteredItems()" 
                    v-bind:key="item.id"
                    v-bind:item="item"
                    v-on:onDelItem="deleteItem"
                    
                />              
           </ul>
        </div>
    </li>
</template> 

<script>
import GroupItem from './GroupItem'
    export default {
        components: {
            GroupItem
        },
        props: ['items','filterGroup'],      
        data(){
            return {
                hovered: false
            }
        },
        methods: {
            dragOver(evt) {
                console.log('dragOver')
                evt.preventDefault()
            },
            dragEnter() {
                console.log('enter')
                this.hovered=true
            },
            dragLeave() {
                console.log('leave')
                this.hovered=false
            },
            dragDrop() {
                console.log('drop')
                this.hovered=false
            },
            filteredItems() {
               if(this.filterGroup === 'done'){
                    return this.items.group.filter(item => item.completed === true)
               }
               if(this.filterGroup === 'name'){
                    return this.items.group
               }
               
            },
            deleteItem(id){
                this.$emit('onDelItem', id, this.items.id)               
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
    .group {
        display: flex;
        flex-direction: column;
        width: 200px;
        height: 150px;      
        background:#f0f4c3 ;       
        margin: 1.2rem 0.6rem;
        border: 0.1rem solid #f0f4c3;
        border-radius: 5px;
    }
        .hovered {
            box-shadow: 0 0 8px rgba(224, 205, 255, 0.801);
        }
        .group:first-child {
            margin: 1.2rem 0.6rem 1.2rem 1.2rem;
        }
        .group__header {           
            width: 100%;
            background: #fff;            
            color: #90caf9;
            display: flex;
            justify-content: space-between;
        }   
            .flex-center {
                display:flex;
                justify-content: center;
                align-items: center;
            }
            .group__title {
                flex-grow: 1;
            }
            .group__controls {
                padding: 0 0.2rem;
            }
            .delete-button {
                position: relative;
                top: 0;
                left: 0;
                width: 20px;
                height:20px;
                background: #ffcdd2 ; 
                border-radius: 50%;
                margin: 0.4rem 0;
            }
                .delete-button:hover {
                    cursor: pointer;
                    box-shadow: 0 0 5px rgba(255, 205, 210, 0.651);
                    background: rgba(255, 205, 210, 0.616);
                }
                .delete-button:active {
                    top: 2px;
                    box-shadow: 0 0 0;
                }
        .group__body {
            flex-grow: 1;           
            color: rgba(0, 0, 0, 0.61);
            overflow-y: scroll;                     
        }
        .group__body::-webkit-scrollbar {width:0px;}

            .group__list {
                padding: 0;

            }
</style>