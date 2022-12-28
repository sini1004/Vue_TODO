<template>
  <div class="inputBox">
    <input 
      class="shadow"
      type="text" 
      placeholder="Please enter a task to do." 
      v-model="newTodoItem" 
      v-on:keyup.enter="addTodo"
    >
    <span v-on:click="addTodo" class="addcontainer">
      <i class="fa-solid fa-plus"></i>
    </span>

    <!-- modal popup -->
    <AlertModal v-if="showModal">
      <h3 slot="header">확인!</h3>
      <span slot="footer">
        내용을 입력해주세요.
        <i class="fa-solid fa-circle-xmark closeModalBtn" v-on:click="showModal = false"></i>
      </span>
      <!-- <button class="modal-default-button" @click="$emit('close')"> OK </button> -->
    </AlertModal>
  </div>
</template>

<script>
import AlertModal from './common/AlertModal.vue';

export default {
  data(){
    return {
      newTodoItem:'',
      showModal: false
    };
  },
  methods: {
    addTodo(){
      // localStorage.setItem(this.newTodoItem, this.newTodoItem);
      // console.log('클릭', this.newTodoItem);
      if(this.newTodoItem !== ''){
        let value = this.newTodoItem && this.newTodoItem.trim();
        // localStorage.setItem(value, value);
        this.$emit('addTodo', value);
        this.clearInput();
        // this.newTodoItem(); // 분리 단일 책임 원칙
      } else {
        this.showModal = true;
      }
    },
    clearInput(){
      // 인풋박스 입력 후 초기화
      this.newTodoItem = '';
    }
  },
  components: {
    AlertModal: AlertModal
  }
}
</script>

<style scoped>
  .inputBox { 
    height: 50px;
    line-height: 50px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 30px;
  }
  input {
    width: calc(90% - 50px);
    border-radius: 30px;
    border: none;
    padding: 0 20px;
    font-size: 1rem;
  }
  input:focus {
    outline: none;
  }
  .addcontainer {
    background: #6c1eb6;
    color: white;
    font-size: 1.2rem;
    width: 50px;
    border-radius: 50px;
  }
  i {
    vertical-align: middle;
    transition: .4s ease-in;
  }
  i:hover {
    transform: rotate(90deg);
  }
  .closeModalBtn {
    color: #333;
  }
</style>