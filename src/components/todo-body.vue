<template>
    <div>
          <h2> Please enter your to do list items</h2>
        <input type="text"  id="inputArea" v-model="input">
        <button v-on:click="addTodo"  id="addButton">Add</button> <br>
        <div v-for="item in todoList" :key="item.id" id="todoListParent">
            <div>
                <i class="fa-solid fa-check"  @click="e => e.target.classList.toggle('checked')"></i>
                <span class="item" >{{item}}</span>
            </div>
            
            <i v-on:click="deleteItem" class="fa-solid fa-trash"></i>
        </div>
    </div>
</template>

<script>




export default {
    data () {
        return {
          input:"",
          todoList:[],
          
      
         
        

        }
    },
    methods:{
        addTodo:function(){
            this.todoList.push(this.input)
            this.input=""
        },
        deleteItem:function(event){
        event.target.parentElement.remove()
        },
      
        

    },


     
}
</script>

<style scoped>

        /* Input Area Styling */
#inputArea{
    width: 25rem;
    height: 2rem;
    border-radius: 0.4rem;
    border: none;
    padding-left: 0.2rem;
    font-size: 1.05rem;

   
}
#inputArea:focus{
    outline: none
}

    /* Buttons styling */
#addButton{
    margin-left:0.3rem;
    width: 4rem;
    height: 2rem;
    border-radius: 0.4rem;
    border: none;
    font-size: 1.05rem;
    cursor: pointer;

}
#addButton:active{
    transform: scale(0.9);
    font-weight: 600;
}

    /* Todo List items Styling */
#todoListParent{
    padding: 0 0.5rem;
    margin: 1rem auto;
    display: flex;
    justify-content: space-between;
}

#todoListParent .item{
    margin-left:1rem ;
    font-size:1.5rem ;
}

.checked{
    color:green;
    font-size:2rem ;
}

</style>