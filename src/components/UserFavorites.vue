<template>
  <div >
    <span>Избранное</span>
    <div class="box-favorites">
      <span>Маги: {{favoriteMag}}</span>
      <span>Маглы: {{favoriteMagl}}</span>
    </div>
  </div>
</template>

<script>
export default {
props:{
  favoriteMag:{
    type:Number,
    default:0,
  },
  favoriteMagl:{
    type:Number,
    default:0,
  }
}
}
</script>

<style scoped>
.box-favorites{
  display: flex;
  flex-direction: column;
}
.box-favorites span{
  margin-top: 15px;
}
</style>