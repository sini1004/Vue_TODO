<template>
  <div>
    <TransitionGroup name="list" tag="ul">
      <li class="shadow" v-for="(todoItem, index) in propsdata" :key="index">
        <span><i class="checkBtn fa-solid fa-check"></i></span>
        <span class="todolist">{{ todoItem }}</span>
        <span class="removeBtn" @click="removeTodo(todoItem, index)"><i class="fa-solid fa-trash"></i></span>
      </li>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  props:['propsdata'],
  // data(){
  //   return{
  //   // Storage 내용을 넣을 빈 배열 생성
  //   todoItems:[]
  //   }
  // },
  // created: function(){
  //   if(localStorage.length>0){
  //     for(let i = 0; i < localStorage.length; i++){
  //       this.todoItems.push(localStorage.key(i));
  //     }
  //   }
  // },
  methods: {
    removeTodo:function(todoItem, index){
      this.$emit('removeTodo', todoItem, index);
      // localStorage.removeItem(todoItem);
      // this.todoItems.splice(index, 1);
      // console.log('키 : ' + index + ' 밸류 : ' + todoItem)
    }
  }
}
</script>

<style scoped>
ul {
  margin: 0;
  padding: 0;
}
ul li {
  display: flex;
  height: 50px;
  line-height: 50px;
  background: white;
  margin: 1rem 0;
  border-radius: 30px;
  padding: 0 20px;
  text-align: left;
}
.checkBtn {
  margin-right: 10px;
  color: #8425de;
}
.todolist {
  white-space: normal;
  overflow: hidden;
  text-overflow: ellipsis;
}
.removeBtn {
  margin-left: auto;
  color: #8425de;
}
.removeBtn i {
  transition: .4s ease-in;
}
.removeBtn i:hover {
  transform: scale(1.2);
}

/* TransitionGroup */
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
</style>