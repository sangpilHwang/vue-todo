<template>
  <div>
      <ul>
        
        <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
          <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
          v-on:click="toggleComplete(todoItem, index)"></i>
          <span v-bind:class="{textCompleted: todoItem.completed}"><!-- textCompleted클래스를 todoItem.completed의 불리언 값에 따라 붙여줌 -->{{ todoItem.item }}</span>
          <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
            <i class="fas fa-trash-alt"></i>
          </span>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  props: ['propsdata'],
  
  methods:{
    removeTodo: function(todoItem, index){
      console.log(todoItem, index);
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1); //splice: 기존있는 배열을 지우고 변경된 배열을 return
      
    },
  toggleComplete: function(todoItem, index){
    todoItem.completed = !todoItem.completed;
    // locaStorage 갱신
    localStorage.removeItem(todoItem.item);
    localStorage.setItem(todoItem.item, JSON.stringify(todoItem)); // JSON.stringify: 객체를 string화 해서 localStorage에 저장할 수 있도록 형 변환.
    console.log(index);
    
  }   
  }

}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  border-radius: 5px;
  background: white;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

</style>