<template>
  <div id="app">
    <header id="pageHeader">
      Список задач
    </header>
		<article id="mainArticle">
     
    </article>
		<nav id="mainNav">
      <div class="button">
        Создать новую задачу
      </div>
      <div class="button">
        Создать новый список задач
      </div>
    </nav>
	<footer id="pageFooter">
    
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
 
  #pageHeader {
    grid-area: header;
    background: #bbdefb; 
    color: #fff;
    font-size: 35px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #pageFooter {
      grid-area: footer;
      background: #bbdefb  

  }
  #mainArticle {
      grid-area: article;
      background: #fff ;
  }
  #mainNav {
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
      box-shadow: 2px 2px 5px rgba(48, 134, 126, 0.658);
    }
    .button:active {
      top: 2px;
    }

</style>
