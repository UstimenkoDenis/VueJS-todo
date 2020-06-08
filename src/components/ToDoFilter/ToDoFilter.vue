<template>
    <div class="filter">
        <div class="filter__buttons">
            <div 
                class="filter__button-title button-filter flex-center"
                v-on:click = "filterByName"
            >
                Название
            </div>
            <div 
                class="filter__button-done button-filter flex-center"
                v-on:click = "filterByDone"
            >
                Выполнены 
            </div>
        </div>        
        <input 
            class = "filter__input"
            type="text"  
            v-model ="text"
           
        >

    </div>        
</template>   
<script>
export default {
    data() {
        return {
            text: null
        }
    },
    methods:{
      filterByName() {
          return this.$emit('filterByName')
      },
      filterByDone() {
          return this.$emit('filterByDone')
      },
    },
    watch: {
        text(value) {
            //  console.log(value)
           return  this.$emit('term', value)
        }
    }
}
</script>
<style>
    .filter {
        flex-grow: 1;
        display: flex; 
        flex-wrap: wrap;     
    }
    .filter__buttons {
        display: inline-flex;
    }
    @media (max-width: 575px) {
        .filter__input {
            margin-top: 10px;                
        }
        .filter__buttons {
            margin-top: 10px;            
        }
    }
        .button-filter {
            position: relative;
            top: 0;
            left: 0;
            box-sizing: inherit;
            border-radius: 3px;
            color: #fff;
            padding: 3px 5px;
            margin: 0 1.2rem 0 0px;           
        }
            
        .filter__button-title {           
            background: #ffcdd2;            
        }
            .filter__button-title:hover {
                cursor: pointer;
                box-shadow: 0 0 5px rgba(211, 129, 137, 0.7);
                background: rgb(255, 205, 210, 0.7);
            }
            .filter__button-title:active {
                top: 2px;
                box-shadow: 0 0 0;
            }
        .filter__button-done {
            background: #e1bee7;                   
        }  
            .filter__button-done:hover {
                cursor: pointer;
                box-shadow: 0 0 5px rgba(161, 110, 170, 0.699);
                background: rgba(225, 190, 231, 0.7);
            }    
            .filter__button-done:active {
                top: 2px;
                box-shadow: 0 0 0;
            }     
        .filter__input {
            min-width: 300px;
            display: block;
            color: #90caf9;
            flex-grow: 1;                 
            border: 1px solid #90caf9;
  
        }  
            .filter__input:active {
                border: 1px solid #588ebb;
            }

</style>