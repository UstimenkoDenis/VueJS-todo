<template>
  <div id="app">
    <header id="page-header">
      Список задач
    </header>
		<article id="main-article">
      <div class="tasks">
        <div class="tasks__header">
          Первоочередные задачи
        </div>
        <ul class="tasks__body">
          
        </ul>
      </div>
      <div class="task-list">
        <div class="task-list__header">
          Списки задач
        </div>
        <ul class="task-list__body">

        </ul>
      </div>
    </article>
		<nav id="main-nav">
      <div class="button">
        Создать новую задачу
      </div>
      <div class="button">
        Создать новый список задач
      </div>
    </nav>
	<footer id="page-footer">
    ustimenkodenis@mail.ru
  </footer>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
   
  }
}
</script>

<style>
  #app {
    display: grid;
    grid-template-areas:
    "header header header"
    "nav article article"
    "footer footer footer";
    grid-template-rows: 80px 1fr 70px;
    grid-template-columns: 20% 1fr 15%;
    grid-row-gap: 10px;
    grid-column-gap: 10px;
    height: 100vh;
    margin: 0;
    padding: 0;
  }

  @media (max-width: 575px) {
      #app {
          grid-template-areas:
          "header"
          "nav"
          "article"          
          "footer";
          grid-template-rows: 30px 120px 1fr 30px;
          grid-template-columns: 1fr;
          
      }
      .button {
        font-size: 8px;
      }
  }
  
  header, footer, article, nav, div {
      padding: 1.2rem;
      border-radius: 5px;
  }
 
  #page-header {
    grid-area: header;
    background: #bbdefb; 
    color: #fff;
    font-size: 35px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #page-footer {
    grid-area: footer;
    background: #bbdefb;  
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    font-size: 25px;
  }
  #main-article {
    grid-area: article;
    background: #fff ;
    display: grid;
    grid-template-areas:
    "tasks"
    "taskList";
    grid-template-rows: 0.5fr 0.5fr;
    grid-template-columns: 1fr;
    grid-row-gap: 10px;
    height: 100vh;
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
      }
      .tasks__body {
        flex-grow: 1;
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
      }
      .task-list__body {
        flex-grow: 1;
      }
  #main-nav {
    grid-area: nav;
    background: #b2dfdb;
  }
    .button {
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
      .button:last-child {
        margin-top: 7px;
      }
    .button:hover {
      cursor: pointer;
      box-shadow: 0 0 5px rgba(48, 134, 126, 0.658);
      background: #80cbc381;
    }
    .button:active {
      top: 2px;
       box-shadow: 0 0 0;
    }


</style>
