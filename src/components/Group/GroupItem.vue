<template>
    <li class="group-item">
        <div class="group-item__header">
            <div class="group-item__title">
                {{item.title}}
            </div>
            <div class="group-item__controls">
                <input class="item-checkbox" type="checkbox">
                <div  v-on:click="toggle=!toggle" class="item-open-button"></div>  
                <div class="item-delete-button"></div>  
            </div>    
        </div>
        <div v-bind:class="{opened: toggle}" class="group-item__body toggle">
           {{item.task}}
        </div>
    </li>
</template>

<script>
export default {
    props: ['item'],
    data () {
        return {
            toggle: false
        }
    },
   
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
        .group-item__header {
            padding: 0.2rem 0.2rem 0 0.3rem;
            display: flex;
            height: 30px;
            align-items: center;
            justify-content:space-between;
        }
            .group-item__title {
                display: flex;
                justify-content: center;
                align-items: center;
            }
            .group-item__controls {
                display: flex;
                justify-content: center;
                align-items: center;
                padding: 0 0.2rem;
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
            padding: 0.4rem 0.2rem 0 0.3rem;
             background: #fff; 
        }
            .opened {
                height: 100px;
            }
</style>