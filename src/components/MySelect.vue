<template>
  <div class="select-box">
    <select :value="modelValue"  class="my-select">
      <option disabled value="none">Выберите из списка</option>
      <option v-for="option in options"
              :key="option.id"
              :value="option.value">
        {{option.name}}
      </option>
    </select>
  </div>

</template>

<script>
export default {
  props:{
    modelValue:{
      type:String,
  },
    options:{
      type:Array,
      default: () => []
    }
  },
}
</script>

<style scoped>
.my-select{
  width: 200px;
  height: 33px;
  outline: none;
  border: none;
}
.select-box{
  display: flex;
  flex-direction: column;
}
.select-box span{
  color: #eca900;
  margin-bottom: 7px;
  font-size: 20px;
}
</style>