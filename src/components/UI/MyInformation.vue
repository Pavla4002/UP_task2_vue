<template>
  <div v-if="showInfo" class="show" >
    <div class="favorites">
   <user-favorites :favoriteMag ="favoriteMag1" :favoriteMagl ="favoriteMagl1" />

    </div>
    <my-name>
      {{ userA.fam}} {{ userA.name}} {{ userA.otch}}
    </my-name>
  </div>
</template>

<script>
import UserFavorites from "@/components/UserFavorites";
import MyName from "@/components/UI/MyName";
export default {
  components: {MyName,UserFavorites},

  props:{
    userA:{
      type:Object,
    },
    showInfo:{
      type:Boolean,
      default:false
    },
    favoriteMag1:{
      type:Number,
      default: 0
    },
    favoriteMagl1:{
      type:Number,
      default: 0
    },

  },

}
</script>

<style scoped>
.show{
  display: flex;
  justify-content: space-between;
  width: 77%;
  margin: 0 auto;
  /*background-color: #fff;*/
  height: 100px;
  color: white;
}
</style>
