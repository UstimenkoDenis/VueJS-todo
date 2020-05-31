<template>
    <li class="card">
        <div class="card__header flex-between">
            <div class="card__title flex-center">
                {{card.title}}
            </div>
            <div class="card__controls">
                <input class="checkbox" type="checkbox">
                <div class="delete-button"></div>  
            </div>                     
        </div>
        <div class="card__body">
            {{card.task}}
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
    }
}
</script>


<style>
    .card {
        display: flex;
        flex-direction: column;
        width: 200px;
        height: 150px;      
        background:#f0f4c3 ;       
        margin: 1.2rem 0.6rem;
        border: 0.1rem solid #f0f4c3;
        border-radius: 5px;
    }
        .card:first-child {
            margin: 1.2rem 0.6rem 1.2rem 1.2rem;
        }
        .card__header {
            width: 100%;
            height: 30px;
            background: #fff;
            color: #90caf9;           
        }   
            .card__title {
                flex-grow: 1;
            }
            .card__controls {
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
        .card__body {
            flex-grow: 1;
            padding: 0.8rem;
            color: rgba(0, 0, 0, 0.61)
        }
</style>