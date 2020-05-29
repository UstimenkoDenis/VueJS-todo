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
          <div class="tasks__header-filter">
            <input class = "input" type="text">
          </div>
        </div>
        <ul class="tasks__body">
          
        </ul>
      </div>
      <div class="task-list">
        <div class="task-list__header">
          <div class="task-list__header-title">
            Списки задач
          </div>
          <div class="task-list__header-filter">
            <input class = "input" type="text">
          </div>
        </div>
        <ul class="task-list__body">

        </ul>
      </div>
    </article>
		<nav class="main-nav">
      <div class="button">
        Создать новую задачу
      </div>
      <div class="button">
        Создать новый список задач
      </div>
    </nav>
	<footer class="page-footer">
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
    height: 100vh;
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
      .button {
        font-size: 8px;
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
        padding: 0;
      }
        .tasks__header-title {
          display:inline-block;
          padding: 1.2rem 1.2rem 0 1.2rem;
        }
        .tasks__header-filter {
          display: inline-flex;
          flex-wrap: wrap;
          padding: 1rem 1.2rem 0 1.2rem;
        }
        .input {
          min-width: 25rem;
          color: #90caf9
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
        padding: 0;
      }
        .task-list__header-title {
          display:inline-block;
          padding: 1.2rem 1.2rem 0 1.2rem;
        }
        .task-list__header-filter {
          display: inline-flex;
          flex-wrap: wrap;
          padding: 1rem 1.2rem 0 1.2rem;
        }
      .task-list__body {
        flex-grow: 1;
      }
  .main-nav {
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
