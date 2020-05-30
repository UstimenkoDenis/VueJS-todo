<template>
    <li class="group">
        <div class="group__header">
            <div class="group__title">
                {{}}
            </div>
            <div class="group__controls">
                <input class="checkbox" type="checkbox">
                <div class="delete-button"></div>  
            </div>                     
        </div>
        <div class="group__body">
           <ul class="group__list">
             
               <GroupItem
                    v-for="item in items" 
                    v-bind:key="item.id"
                    v-bind:item="item"/>              
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
        props: {
            items: {
                type: Object,
                required: true
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
        .group:first-child {
            margin: 1.2rem 0.6rem 1.2rem 1.2rem;
        }
        .group__header {
            width: 100%;
            height: 30px;
            background: #fff;
            color: #90caf9;
            display: flex;
            justify-content: space-between;
        }   
            .group__title {
                flex-grow: 1;
                display:flex;
                justify-content: center;
                align-items: center;

            }
            .group__controls {
                display: flex;
                justify-content: center;
                align-items: center;
                padding: 0 0.2rem;
            }
            .checkbox {
                width: 20px;
                height: 20px;
            }
            .delete-button {
                width: 20px;
                height:20px;
                background: #ffcdd2 ; 
                border-radius: 50%;
            }
        .group__body {
            flex-grow: 1;
           
            color: rgba(0, 0, 0, 0.61);
          
        }
            .group__list {
                padding: 0;
            }
</style>