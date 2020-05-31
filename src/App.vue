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
          <ToDoFilter/>
        </div>
        <div class="tasks__body">
          <CardList v-bind:cardsData="cardsData"/>     
        </div>         
      </div>
      <div class="group-list">
        <div class="group-list__header">
          <div class="group-list__header-title">
            Списки задач
          </div>
          <ToDoFilter/>
        </div>
        <div class="group-list__body">
          <GroupList v-bind:groupData="groupData"/>
        </div>
      </div>
    </article>
		<nav class="main-nav">
      <div class="menu-button">
        Создать новую задачу
      </div>
      <div class="menu-button">
        Создать новый список задач
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
  data() {
    return {
      cardsData: [
        {id: 1, title: "Купить", task: "Хлеб, молоко", completed: false},
        {id: 2, title: "Заплатить", task: "Кредит", completed: false},
        {id: 3, title: "Прочитать", task: "JS Николас Закас", completed: false},
        {id: 4, title: "Посмотреть", task: "Netflix", completed: false}        
      ],
      groupData: [
                  { title: "Купить",
                    group: [
                        {id: 5, title: "Купить", task: "Книги", completed: false},
                        {id: 6, title: "Name2", task: "Body2", completed: false},
                        {id: 7, title: "Name1", task: "Body1", completed: false},
                        {id: 7, title: "Name1", task: "Body1", completed: false}
                    ]
                  },
                  { title: "Прочитать",
                    group: [
                            {id: 8, title: "Name1", task: "Body1", completed: false},
                            {id: 9, title: "Name2", task: "Body2", completed: false},
                            {id: 10, title: "Name1", task: "Body1", completed: false}
                    ]
                  }                             
      ]          
    }
  }
}
</script>

<style>
  .app {
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
      font-size: 20px;
      transition: cubic-bezier(0.075, 0.82, 0.165, 1);
    }
      .menu-button:last-child {
        margin-top: 7px;
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

</style>
