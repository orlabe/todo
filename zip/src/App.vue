<!--cd todo-vue   npm run dev 43.04 -->

<template>

  <div id="app" class="container">
    <img src="https://hg1.funnyjunk.com/pictures/Pink+panthers+todo+list+httpwwwyoutubecomwatchvhhhwnrlzrus_40068f_5003366.png" class="logo" >
      <todo-list> </todo-list>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import TodoList from './components/TodoList'


export default {
  name: 'App',
  components: {
    HelloWorld,
    TodoList,
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  background-image: url(https://image.freepik.com/free-photo/white-paper-texture-background-with-soft-pattern_179068-730.jpg);
  
  background-size: cover ;
}

.container {
  max-width: 650px;
  margin: 0 auto;
 border: solid rgb(223, 131, 184) 10px;
 padding: 0 30px;

 

}

.logo {
display: block;
margin: 20px auto;
height: 250px;
width: 575px;;

}
#app {
   font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #c70a68;
  margin-top: 60px;
  font-size: 24px;

}
</style>
