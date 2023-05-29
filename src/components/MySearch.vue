<template>
  <div class="input-box">
    <span class="color-white">Find a character</span>
    <input type="text" :value="inputVal1" class="input-style">
  </div>
</template>

<script>
export default {
props:{
  inputVal1:{
    type:String,
    default:'',
  }
}
}
</script>

<style scoped>
.input-style{
  width: 200px;
  height: 30px;
  background-color: white;
  outline: none;
  border: none;
}
.input-box{
  display: flex;
  flex-direction: column;
}
.color-white{
  color: #eca900;
  margin-bottom: 7px;
  font-size: 20px;
}
</style>