<template>
  <div class="app">
    <header class="page-header">
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
          <Card/>
           <Card/>
        </div>         
      </div>
      <div class="task-list">
        <div class="task-list__header">
          <div class="task-list__header-title">
            Списки задач
          </div>
          <ToDoFilter/>
        </div>
        <div class="task-list__body">
          <CardList/>
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
	<footer class="page-footer">
    ustimenkodenis@mail.ru
  </footer>
  </div>
</template>

<script>
import ToDoFilter from './components/ToDoFilter/ToDoFilter'
import Card from './components/Card/Card'
import CardList from './components/CardList/CardList'
export default {
  name: 'App',
  components: {
    ToDoFilter,
    Card,
    CardList
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
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .page-footer {
    grid-area: footer;
    background: #bbdefb;  
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    font-size: 25px;
  }
  .main-article {
    grid-area: article;
    background: #fff ;
    display: grid;
    grid-template-areas:
    "tasks"
    "taskList";
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
        display: flex;        
      }
    .task-list {
      grid-area: taskList;
      display: flex;
      flex-direction: column;
      padding: 0;
      margin: 0;
      border: 1px solid #bbdefb;
      border-radius: 5px;      
    }
      .task-list__header {
        color:#90caf9 ;
        font-size: 20px;
        padding: 0;
        display: flex;
        flex-wrap: wrap;      
        padding: 1.2rem 1.2rem 0 1.2rem;
      }
        .task-list__header-title {
          display:inline-block;   
          margin-right: 1.2rem;   
        }       
      .task-list__body {
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
