<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <!-- <TodoInput v-on:addTodoItem="addOneItem"></TodoInput> -->
    <TodoInput></TodoInput>
    <TodoList v-bind:propsdata="todoItems" 
    v-on:removeItem="removeOneItem" 
    v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItem"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoFooter from './components/TodoFooter.vue'
import TodoList from './components/TodoAppList.vue'

export default {
  data: function(){
    return {
      todoItems: []
    }
  },
  methods: { // mutations
    // addOneItem(todoItem){
    //   const obj={completed: false, item: todoItem};
    //   // 저장하는 로직
    //   localStorage.setItem(todoItem, JSON.stringify(obj));
    //   this.todoItems.push(obj);
    // },
    removeOneItem(todoItem,index){
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleOneItem(toggleItem,index){
      this.todoItems[index].completed = !this.todoItems[index].completed
      localStorage.removeItem(toggleItem.item);
      localStorage.setItem(toggleItem.item, JSON.stringify(toggleItem));
    },
    clearAllItem(){
      localStorage.clear();
      this.todoItems = [];
    }
  },
    // 인스턴스가 생성될 때 호출 됨
  // created(){
  //   if (localStorage.length > 0){
  //     for (let i = 0; i < localStorage.length; i++){
  //       if (localStorage.key(i) !== "loglevel:webpack-dev-server"){
  //         this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
  //       }
  //     }
  //   }
  // },
  components: {
    TodoHeader,
    TodoFooter,
    TodoList,
    TodoInput
  },
}
</script>

<style>
body {
  text-align: center;
  background-color: #F6F6F6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
}

</style>