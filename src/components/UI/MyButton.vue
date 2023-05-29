<template>
        <button class="button-box"><slot></slot></button>
</template>

<script>
export default {

}
</script>

<style scoped>
.button-box{
  width: 150px;
  height: 30px;
}
button{
  background-color: white;
  border: none;
}
</style>