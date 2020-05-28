<template>
  <div id="app">
    <header id="pageHeader">
      Header
    </header>
		<article id="mainArticle">
      Article
    </article>
		<nav id="mainNav">
      Nav
    </nav>
	<footer id="pageFooter">
    Footer
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
          grid-template-rows: 30px 30px 1fr 30px;
          grid-template-columns: 1fr;
      }
  }
  
  header, footer, article, nav, div {
      padding: 1.2rem;
      border-radius: 0.3rem;
  }
 
  #pageHeader {
    grid-area: header;
    background: #bbdefb 

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

</style>
