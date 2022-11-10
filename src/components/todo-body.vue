<template>
    <div>
          <h2> Please enter your to do list items</h2>
        <input type="text"  id="inputArea" v-model="todoItem.input"><br>
        <input type="datetime-local"  id="deadline" v-model="todoItem.deadLine"><br>
        <button v-on:click="addTodo"  id="addButton">Add</button> <br>
        <div v-for="item in todoList" :key="item.name" id="todoListParent">
            <div v-bind:id="item.id" v-bind:class="item.class">
                <i class="fa-solid fa-check" @click="e => e.target.parentElement.classList.toggle('line')" ></i>
                <span class="item"  @click="e => e.target.parentElement.classList.toggle('line')"  >{{item.input}}</span>
                <span class="item" @click="e => e.target.parentElement.classList.toggle('line')">{{item.deadLine}}</span>
            </div>
            
            <i v-on:click="deleteItem" class="fa-solid fa-trash"></i>
        </div>
    </div>
</template>

<script>


 


export default {
    data () {
        return {
            todoItem:{
              input:"",
              deadLine:"",
              isPast:"",
              id:"",
              class:"aaa"
            },
          
          todoList:[],
          
        
         
        

        }
    },
    methods:{
        addTodo:function(){
            this.todoItem.deadLine = this.todoItem.deadLine.replace("T", " ");
            // console.log(this.deadLine)
            this.todoItem.isPast = Date.now() > new Date(this.todoItem.deadLine).getTime();
            //  console.log(this.todoItem.isPast)
            this.todoItem.id=Date.now()
            // console.log(this.id)
            if(this.todoItem.input.trim() ==="" || this.todoItem.input === null){
                alert("formu lütfen doldurunuz")
            }
            else if(this.todoItem.isPast){
                alert("geçerli bir tarih giriniz")
            }
            else{
             this.todoList.push({...this.todoItem},
             
             
                
            )}
            localStorage.setItem("todoList", JSON.stringify([...this.todoList]))
             this.input=""
       
            
        },
        deleteItem:function(event){
        event.target.parentElement.remove()
        },
        
        

    },
 
    beforeMount(){
      
   
        this.todoList= JSON.parse(localStorage.getItem("todoList"))  || '[]';

        this.todoList.map((item) => new Date(item.deadLine).getTime() < Date.now()  &&  (item.class="line") );
         localStorage.setItem("todoList", JSON.stringify([...this.todoList]));

      
    },
    // mounted(){
    //    this.todoList= JSON.parse(localStorage.getItem("todoList"))
    // },
    updated(){
        localStorage.setItem("todoList", JSON.stringify([...this.todoList]));
    }
    


     
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


#deadline{
    margin:1rem auto;
     width: 25rem;
    height: 2rem;
    border-radius: 0.4rem;
    border: none;
    padding-left: 0.2rem;
    font-size: 1.05rem;
}

#inputArea:focus,#deadline:focus {
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

#todoListParent .line{
    background-color:green ;
}
#todoListParent .line .item{
    text-decoration: line-through;
}

#todoListParent .line .fa-check{
     color:red;
    font-size:2rem ;
}


</style>

