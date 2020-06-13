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
              v-bind:dragId = "dragId"
              @onDelete = "deleteCard"
              @onDragId = "onDragId"
              @dragCardOrItem = "setDragCard"
              @addItemInList = "addItemInCardList"
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
              v-bind:dragId = "dragId"              
              v-bind:cardsData = "cardsData"
              @onDelGroup = "deleteGroup"
              @onDelItem = "deleteItem"
              @addItem = "addItem" 
              @onDragId = "onDragId"
              @dragCardOrItem = "setDragItem"
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
  </div>
</template>

<script>
import ToDoFilter from './components/ToDoFilter/ToDoFilter'
import CardList from './components/CardList/CardList'
import GroupList from './components/GroupList/GroupList'

export default {
  name: 'App',
  components: {
    ToDoFilter,
    CardList,
    GroupList  
  },
  methods: {
    onDragId(id, idGroupFrom) {
     this.dragId = id
     this.idGroupFrom = idGroupFrom    
    },
    setDragCard() {
      this.dragCardOrItem = 'card'      
    },
    setDragItem() {
      this.dragCardOrItem = 'item'     
    },
    setTerm(term) {
      this.term = term
    },
    setGroupTerm(term) {
      this.groupTerm=term     
    },
    filterByName() {
      this.filter = 'name' 
    },
     filterByDone() {
      this.filter = 'done'
    },
    filterGroupByDone() {
      this.filterGroup = 'done'      
    },
    filterGroupByName() {
      this.filterGroup = 'name'
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
    addItem(id, groupId) {
     if(this.dragCardOrItem == 'card') {
        const indexGroup = this.groupData.findIndex((item)=>item.id === groupId)
        const indexCard = this.cardsData.findIndex((item)=> item.id === id)
        const newGroupItems = [...this.groupData[indexGroup].group]
        newGroupItems.unshift(this.cardsData[indexCard])
        this.deleteCard(this.cardsData[indexCard].id) // удаляю из карт
        return (
          this.groupData[indexGroup].group = newGroupItems // добавляю в группу
        )
     } else 
     if(this.dragCardOrItem == 'item') {  
       if(groupId !== this.idGroupFrom)  { // группа - откуда неравно группа -куда
          const indexGroup = this.groupData.findIndex((item)=>item.id === groupId) // индекс группы куда
          const indexGroupFrom = this.groupData.findIndex((item)=>item.id === this.idGroupFrom) // индекс группы откуда
          const indexItem = this.groupData[indexGroupFrom].group.findIndex((item)=> item.id === id) // индекс item откуда
          const newGroupItems = [...this.groupData[indexGroup].group]
          newGroupItems.unshift(this.groupData[indexGroupFrom].group[indexItem])
          this.deleteItem(id, this.idGroupFrom) // удаляю из списка группы
          return (
            this.groupData[indexGroup].group = newGroupItems // добавляю в группу
          )
       }    
        
     }
      
    },
    addItemInCardList(id) {
      if (this.dragCardOrItem === 'item') {       
        const indexGroupFrom = this.groupData.findIndex((item)=>item.id === this.idGroupFrom) // индекс группы откуда
        const indexItem = this.groupData[indexGroupFrom].group.findIndex((item)=> item.id === id) // индекс item откуда
        const newCardsData = [...this.cardsData]
        newCardsData.unshift(this.groupData[indexGroupFrom].group[indexItem]) 
        this.deleteItem(id, this.idGroupFrom) // удаляю из списка группы
        return (
          this.cardsData = newCardsData // добавляю в список
        )
      }

    },
    addCard(title, description) { 
      if(title !== null){     
        const id = `f${(+new Date).toString(16)}`;  // уникальный id 
        const newCard = {
          id,
          title,
          description,
          completed: false
        }
        const newCardsData = [...this.cardsData]
        newCardsData.unshift(newCard)      
        return (
          this.cardsData = newCardsData
        )
      }
      
    },   
    deleteCard(id) {  
        const index = this.cardsData.findIndex((elem)=>elem.id === id)
        const before = this.cardsData.slice(0,index)
        const after = this.cardsData.slice(index+1)
        const newCardsData = [...before,...after]
        this.cardsData = newCardsData   
        this.modalApply = false                      
    },
    addGroup(title) { 
      if(title !== null){
        const id = `f${(+new Date).toString(16)}`;  // уникальный id  
        const newGroup = {
          id,
          title,
          group:[]  
        }
        const newGroupData = [...this.groupData]
        newGroupData.unshift(newGroup)      
        return (
          this.groupData = newGroupData
        )
      }       
    },
    deleteGroup(id) {
        const index = this.groupData.findIndex((elem)=>elem.id === id)
        const before = this.groupData.slice(0,index)
        const after = this.groupData.slice(index+1)
        const newGroupData = [...before,...after]
        this.groupData = newGroupData                        
    },
    deleteItem(id, idGroup) {
        const indexGroup = this.groupData.findIndex((elem)=>elem.id === idGroup)
        const index = this.groupData[indexGroup].group.findIndex((elem)=>elem.id === id)         
        const before = this.groupData[indexGroup].group.slice(0,index)
        const after = this.groupData[indexGroup].group.slice(index+1)
        const newGroupList = [...before,...after]         
        this.groupData[indexGroup].group = newGroupList       
    }       
  },    

   
  data() {
    return {
      dragId: 0,
      idGroupFrom: 0,
      dragCardOrItem:'',
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
      groupData: []         
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
    grid-template-columns: 20% 1fr 1fr;
    grid-row-gap: 10px;
    grid-column-gap: 10px;
    min-height: 100vh;
    margin: 0;
    padding: 0;    
  }

  @media (max-width: 768px) {
      .app {
        grid-template-areas:
        "header"
        "nav"
        "article"          
        "footer";
        grid-template-rows: 30px 0.3fr 100% 30px;
        grid-template-columns: 1fr;
        font-size: 30px;
      }       
  }
  .flex-center {
    display: flex;
    justify-content: center;
    align-items: center;
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
      min-width: 300px;    
    }
      .tasks__header {
        color:#90caf9 ;
        font-size: 20px;        
        display: flex;
        flex-wrap: wrap;
        padding: 1rem;
        align-items: center;
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
      min-width: 300px;    
    }
      .group-list__header {
        color:#90caf9 ;
        font-size: 20px;
        padding: 0;
        display: flex;
        flex-wrap: wrap;      
        padding: 1rem;
        align-items: center;
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
  @media (max-width: 575px) {
      .main-nav {
          padding-top: 0;         
      }      
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
   
    @media (max-width: 768px) {
      .menu-button {
        font-size: 24px;       
      }     
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
       
        width: 100%;
        min-height: 30px;
        font-size: 20px;
        display: block;
        color: #90caf9;                           
        border: 1px solid #90caf9;
      }
      .main-nav__text-area {
          margin-top: 1.2rem;
          margin: 10px auto;
          width: 100%;
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
