<template>
  <div id="container" >
    <todo-header></todo-header>
    <todo-body></todo-body>
  </div>
</template>

<script>

import header from "./components/todo-header.vue"
import body from "./components/todo-body.vue"

export default {
  components:{
    "todo-header": header,
    "todo-body": body,
  }
}
</script>

<style scoped>
#container{

    width: 50vw;
    margin: 3rem auto 0;
    background-color: lightsteelblue;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap:1rem;
    padding: 1rem;
 
}

</style>
