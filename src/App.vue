<template>
  <div class="app">
    <header class="page-header flex-center">
      Список задач
    </header>
		<article class="main-article">      
      <div class="tasks">
        <div class="tasks__header">
          <div class="tasks__header-title">
            Первоочередные задачи
          </div>
          <ToDoFilter
                @term = "setTerm"
                @filterByName = "filterByName"
                @filterByDone = "filterByDone"
          />
        </div>
        <div class="tasks__body">
          <CardList 
              v-bind:cardsData = "cardsData"
              v-bind:term = "term"
              v-bind:filter = "filter"
              @onDelete="deleteCard"
          />     
        </div>         
      </div>
      <div class="group-list">
        <div class="group-list__header">
          <div class="group-list__header-title">
            Списки задач
          </div>
          <ToDoFilter
              @filterByName ="filterGroupByName"
              @filterByDone ="filterGroupByDone"
              @term = "setGroupTerm"
          />
        </div>
        <div class="group-list__body">
          <GroupList 
              v-bind:groupData = "groupData"
              v-bind:filterGroup = "filterGroup"
              v-bind:groupTerm = "groupTerm"
              @onDelGroup = "deleteGroup"
              @onDelItem = "deleteItem"
          />
        </div>
      </div>
    </article>
		<nav class="main-nav">
      <div 
        class="menu-button"
        v-on:click="choise=true, inputsBlockVisible=true, textAreaVisible=true, labelTextAreaVisible=true"
      >
        Создать новую задачу
      </div>
      <div 
        class="menu-button"
        v-on:click="choise=false, inputsBlockVisible=true, textAreaVisible=false, labelTextAreaVisible=false"
      >
        Создать новый список задач
      </div>
      <div class="main-nav__inputs" v-show="inputsBlockVisible">
        <label 
            class="main-nav__label" 
            for="title"            
        >Что нужно сделать?
        </label>
          <input 
              id="title" 
              class="main-nav__input" 
              type="text"               
              v-model="input"              
          >
        <label 
            class="main-nav__label" 
            for="description"
            v-show="labelTextAreaVisible"
        >Описание
        </label>  
          <textarea 
                id="description" 
                class="main-nav__text-area" 
                v-model="textArea"
                v-show="textAreaVisible"
          ></textarea>
          <div 
            class="main-nav__button"
            v-on:click="createElement(choise)"
          >Создать
          </div>
      </div>
    </nav>
    <footer class="page-footer flex-center">
      ustimenkodenis@mail.ru
    </footer> 
   <Modal 
      v-if="modalVisible"
      @close="closeModal"
      @apply="closeModal"
    />
  </div>
</template>

<script>
import ToDoFilter from './components/ToDoFilter/ToDoFilter'
import CardList from './components/CardList/CardList'
import GroupList from './components/GroupList/GroupList'
import Modal from './components/Modal/Modal'

export default {
  name: 'App',
  components: {
    ToDoFilter,
    CardList,
    GroupList,
    Modal
  },
  methods: {
    setTerm(term) {
      this.term = term
    },
    setGroupTerm(term) {
      this.groupTerm=term
      console.log(term)
    },
    filterByName() {
      this.filter = 'name' 
    },
     filterByDone() {
      this.filter = 'done'
    },
    filterGroupByDone() {
      this.filterGroup = 'done'
      console.log(this.filterGroup)
    },
    filterGroupByName() {
      this.filterGroup = 'name'
            console.log(this.filterGroup)

    },   
    createElement(choise){
      if(choise) {       
        this.addCard(this.input, this.textArea)
        this.inputsBlockVisible=false
      } else {
        this.inputsBlockVisible=false
        this.addGroup(this.input)
      } 
    },
    addCard(title, description) {
      const id = this.cardsData.length + 1
      const newCard = {
        id,
        title,
        description,
        completed: false
      }
      const newCardsData = [...this.cardsData]
      newCardsData.unshift(newCard)
      console.log(newCardsData)
      return (
        this.cardsData = newCardsData
      )
      
    },   
    deleteCard(id) {  
      if(confirm('Вы действительно хотите удалить?')){
        const index = this.cardsData.findIndex((elem)=>elem.id === id)
        const before = this.cardsData.slice(0,index)
        const after = this.cardsData.slice(index+1)
        const newCardsData = [...before,...after]
        this.cardsData = newCardsData   
        this.modalApply = false  
      }              
    },
    addGroup(title) {
      const id = this.groupData.length + 1
      const newGroup = {
        id,
        title  
      }
      const newGroupData = [...this.groupData]
      newGroupData.unshift(newGroup)
      console.log(newGroupData)
      return (
        this.groupData = newGroupData
      )
      
    },
    deleteGroup(id) {
      if(confirm('Вы действительно хотите удалить?')){
        const index = this.groupData.findIndex((elem)=>elem.id === id)
        const before = this.groupData.slice(0,index)
        const after = this.groupData.slice(index+1)
        const newGroupData = [...before,...after]
        this.groupData = newGroupData
        console.log(id)
      }           
    },
    deleteItem(id, idGroup) {
       if(confirm('Вы действительно хотите удалить?')){ 
        const indexGroup = this.groupData.findIndex((elem)=>elem.id === idGroup)
        const index = this.groupData[indexGroup].group.findIndex((elem)=>elem.id === id)
         
            const before = this.groupData[indexGroup].group.slice(0,index)
            const after = this.groupData[indexGroup].group.slice(index+1)
            const newGroupList = [...before,...after]           
          
         this.groupData[indexGroup].group = newGroupList 
      }
    }       
  },    

   
  data() {
    return {
      filter:'name',
      filterGroup: 'name',
      term: '',
      groupTerm:'',
      modalApply: false,
      modalVisible: false,      
      input: null,
      textArea: null,
      textAreaVisible: false,
      labelTextAreaVisible: false,
      inputsBlockVisible: false,
      choise: true,
      cardsData: [
        {id: 1, title: "Купить",description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Est fugiat nihil eos vel, ipsam doloremque perferendis architecto possimus saepe obcaecati laborum molestias neque eligendi cum dolore ipsa quod iure. Consectetur.", completed: false},
        {id: 2, title: "Заплатить",description: "Кредит", completed: false},
        {id: 3, title: "Прочитать",description: "JS Николас Закас", completed: false},
        {id: 4, title: "Посмотреть",description: "Netflix", completed: false}        
      ],
      groupData: [
                  { id: 1,
                    title: "Купить",
                    group: [
                        {id: 5, title: "Купить",description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Est fugiat nihil eos vel, ipsam doloremque perferendis architecto possimus saepe obcaecati laborum molestias neque eligendi cum dolore ipsa quod iure. Consectetur.", completed: false},
                        {id: 6, title: "Name2",description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Est fugiat nihil eos vel, ipsam doloremque perferendis architecto possimus saepe obcaecati laborum molestias neque eligendi cum dolore ipsa quod iure. Consectetur.", completed: false},
                        {id: 7, title: "Name1",description: "Body1", completed: false},
                        {id: 8, title: "Name1",description: "Body1", completed: false}
                    ]
                  },
                  { id: 2,
                    title: "Прочитать",
                    group: [
                            {id: 9, title: "Name1",description: "Body1", completed: false},
                            {id: 10, title: "Name2",description: "Body2", completed: false},
                            {id: 11, title: "Name1",description: "Body1", completed: false}
                           
                    ]
                  },
                  { id: 3,
                    title: "Купить",
                    group: [
                        {id: 5, title: "Купить",description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Est fugiat nihil eos vel, ipsam doloremque perferendis architecto possimus saepe obcaecati laborum molestias neque eligendi cum dolore ipsa quod iure. Consectetur.", completed: false},
                        {id: 6, title: "Name2",description: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Est fugiat nihil eos vel, ipsam doloremque perferendis architecto possimus saepe obcaecati laborum molestias neque eligendi cum dolore ipsa quod iure. Consectetur.", completed: false},
                        {id: 7, title: "Name1",description: "Body1", completed: false},
                        {id: 8, title: "Name1",description: "Body1", completed: false}
                    ]
                  },
                  { id: 4,
                    title: "Прочитать",
                    group: [
                            {id: 9, title: "Name1",description: "Body1", completed: false},
                            {id: 10, title: "Name2",description: "Body2", completed: false},
                            {id: 11, title: "Name1",description: "Body1", completed: false}
                           
                    ]
                  }                                   
      ]          
    }
  }
}
</script>

<style>
  .app {
    font-family: 'Roboto', sans-serif;
    display: grid;
    grid-template-areas:
    "header header header"
    "nav article article"
    "footer footer footer";
    grid-template-rows: 80px 1fr 70px;
    grid-template-columns: 20% 1fr 15%;
    grid-row-gap: 10px;
    grid-column-gap: 10px;
    min-height: 100vh;
    margin: 0;
    padding: 0;    
  }

  @media (max-width: 575px) {
      .app {
          grid-template-areas:
          "header"
          "nav"
          "article"          
          "footer";
          grid-template-rows: 30px 120px 1fr 30px;
          grid-template-columns: 1fr;
          
      }
      .menu-button {
        font-size: 8px;
      }
  }
  @media (max-width: 362px) {
      .menu-button {
        font-size: 2px;
      }
  }
  
  .page-header, .page-footer, .main-article, .main-nav {
      padding: 1.2rem;
      border-radius: 5px;
  }
 
  .page-header {
    grid-area: header;
    background: #bbdefb; 
    color: #fff;
    font-size: 35px;  
  }
  .page-footer {
    grid-area: footer;
    background: #bbdefb;  
    color: #fff;
    font-size: 25px;
  }
  .main-article {
    grid-area: article;
    background: #fff ;
    display: grid;
    grid-template-areas:
    "tasks"
    "groupList";
    grid-template-rows: 0.5fr 0.5fr;
    grid-template-columns: 1fr;
    grid-row-gap: 10px;
    margin: 0;
    padding: 0;
  }
    .tasks {
      grid-area: tasks; 
      display: flex;
      flex-direction:column;
      padding: 0;
      margin: 0;
      border: 1px solid #bbdefb;
      border-radius: 5px;   
      min-width: 500px;    
    }
      .tasks__header {
        color:#90caf9 ;
        font-size: 20px;        
        display: flex;
        flex-wrap: wrap;
        padding: 1.2rem 1.2rem 0 1.2rem;
      }
        .tasks__header-title {
          display:inline-block;   
          margin-right: 1.2rem;      
        }
        
      .tasks__body {
        flex-grow: 1;   
           width: 100%;            
      }
    .group-list {
      grid-area: groupList;
      display: flex;
      flex-direction: column;
      padding: 0;
      margin: 0;
      border: 1px solid #bbdefb;
      border-radius: 5px;   
      min-width: 500px;    
    }
      .group-list__header {
        color:#90caf9 ;
        font-size: 20px;
        padding: 0;
        display: flex;
        flex-wrap: wrap;      
        padding: 1.2rem 1.2rem 0 1.2rem;
      }
        .group-list__header-title {
          display:inline-block;   
          margin-right: 1.2rem;   
        }       
      .group-list__body {
        flex-grow: 1;        
      }
  .main-nav {
    grid-area: nav;
    background: #b2dfdb;
  }
    .menu-button {
      position: relative;
      top: 0;
      left: 0;
      background: #80cbc4;
      border-radius: 5px;
      text-align: center;
      color:#fff;
      padding: 7px;
      margin-top: 1rem;
      font-size: 20px;
      transition: cubic-bezier(0.075, 0.82, 0.165, 1);
    }
      
    .menu-button:hover {
      cursor: pointer;
      box-shadow: 0 0 5px rgba(48, 134, 126, 0.658);
      background: rgba(128, 203, 195, 0.506);
    }
    .menu-button:active {
      top: 2px;
      box-shadow: 0 0 0;
    }
    .main-nav__inputs {
      margin-top: 2.2rem;
      text-align: center;
    }
      .main-nav__label {
        color: #fff;
      }
      .main-nav__input {
        margin-top: 1.2rem;
        margin: 10px auto;
        min-width: 100px;
        min-height: 30px;
        font-size: 20px;
        display: block;
        color: #90caf9;                           
        border: 1px solid #90caf9;
      }
      .main-nav__text-area {
          margin-top: 1.2rem;
          margin: 10px auto;
          min-width: 100px;
          min-height: 130px;
          font-size: 20px;
          display: block;
          color: #90caf9;                           
          border: 1px solid #90caf9;
      }
      .main-nav__text-area::-webkit-scrollbar {width:0px;}
      .main-nav__button {
        display: inline-block;
        padding: 0.3rem 0.5rem;
        background: #80cbc4;
        border-color: #90caf9;
        border-radius: 5px;
        color: #fff;
        font-size: 20px;
        margin: 0.7rem auto;
        position: relative;
        top: 0;
        left: 0;
      }
        .main-nav__button:hover {
          cursor: pointer;
          box-shadow: 0 0 5px rgba(48, 134, 126, 0.658);
          background: rgba(128, 203, 195, 0.506);
        }
        .main-nav__button:active {
          top: 2px;
          box-shadow: 0 0 0;
        }

</style>
