<template>
    <li 
        class="group-item"
        draggable="true"
        v-bind:class="{hide: itemHide}" 
        v-on:dragstart="dragStart"    
        v-on:dragend="dragEnd"    
    >
        <div class="group-item__header flex-between">
            <div 
                class="group-item__title flex-center"
                v-bind:class="{done: item.completed}"
            >
                {{item.title}}
            </div>
            <div class="group-item__controls flex-center">
                <input 
                    class="item-checkbox" 
                    v-on:change="item.completed = !item.completed" 
                    type="checkbox"
                >
                <div   
                    class="item-open-button" 
                    v-on:click="toggle=!toggle"
                ></div>  
                <div 
                    class="item-delete-button"
                    v-on:click="$emit('onDelItem', item.id)"
                ></div>  
            </div>    
        </div>
        <div
            class="group-item__body" 
            v-bind:class="{opened: toggle}"
        >
           {{item.description}}
        </div>
    </li>
</template>

<script>
export default {
    props: ['item'],
    data () {
        return {
            toggle: false,
            itemHide: false
        }
    },
    methods: {
        dragStart() {
           setTimeout(()=>{
                this.itemHide = true             
                return (
                    this.$emit('onDragId', this.item.id),
                    this.$emit('dragCardOrItem', 'item')
                )
            },0) 
        },
        dragEnd() {           
                this.itemHide = false             
        }
    }   
}
</script>

<style>
    .group-item {
        width: 100%;
        /* height: 30px; */
        background: #f9fbe7;
        list-style: none;
        margin: 0.1rem 0;        
    }
        .flex-between {
            display: flex;
            align-items: center;
            justify-content:space-between;
        }
        .group-item__header {
            padding: 0.2rem 0.2rem 0 0.3rem;           
            height: 30px;           
        }
            .group-item__controls {
                padding: 0 0.2rem;
            }
                .item-checkbox {
                    
                }
                .item-open-button {
                    position: relative;
                    left: 0;
                    top: 0;
                    width: 14px;
                    height:14px;
                    margin-right: 0.2rem;
                    background: #c8e6c9; 
                    border-radius: 50%;
                }
                .item-open-button:hover {
                    cursor: pointer;
                    box-shadow: 0 0 5px rgba(200, 230, 201, 0.568);
                    background: rgba(200, 230, 201, 0.637);
                }
                .item-open-button:active {
                    top: 2px;
                    box-shadow: 0 0 0;
                }
            .item-delete-button {
                position: relative;
                left: 0;
                top: 0;
                width: 14px;
                height:14px;
                background: #ffcdd2 ; 
                border-radius: 50%;
            }
                .item-delete-button:hover {
                    cursor: pointer;
                    box-shadow: 0 0 5px rgba(255, 205, 210, 0.651);
                    background: rgba(255, 205, 210, 0.616);
                }
                .item-delete-button:active {
                    top: 2px;
                    box-shadow: 0 0 0;
                }
        .group-item__body {
            display: none;
            padding: 0.4rem 0.2rem 0 0.3rem;
            background: #fff; 
            color: rgba(0, 0, 0, 0.61)
        }
            .opened {
                display: block;
                height: 100%;
            }
            .done {
                text-decoration: line-through
            }
</style>