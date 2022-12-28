<template>
  <div>
    <span @click="clearTodo">Clear All</span>
  </div>
</template>

<script>
export default {
  methods:{
    clearTodo(){
      this.$emit('removeAll');
    }
  }
}
</script>

<style>

</style>