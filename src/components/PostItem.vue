<template>
  <div class="post-box">
    <div class="post">
      <div class="box-img" @click="$emit('choice',post)">
        <img src="../assets/img/Нет_фото.png" alt="" class="with-img" v-if="post.image === '' ">
        <img :src="post.image" alt="" class="with-img" v-else>
      </div>
      <span class="name-pers name">{{post.name}}</span>
      <span class="name-pers">Patronus : {{post.patronus}}</span>
      <span class="name-pers">Actor : {{post.actor}}</span>
      <span class="name-pers">House : {{post.house}}</span>
      <my-button class="absolut" v-if="showButton"  @click="$emit('add',post)">
        <my-name @click ="$emit('showValue',$event,post)" class="text-vertical">
          Add to favorites
        </my-name>
      </my-button>

    </div>
  </div>

</template>

<script>
import MyName from "@/components/UI/MyName";
import MyButton from "@/components/UI/MyButton";
export default {
  components: {
    MyButton,
    MyName
  },
  props:{
    post:{
      type:Object,
      required:true
    },
    showButton:{
      type:Boolean,
      default:false
    },
    valueButton:{
      type:String,
      default: 'Add to favorites'
    },

  },

}
</script>

<style scoped>
.post-box{
  flex: 1;
}
.post{
  width: 300px;
  height: 450px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  background-color: #fff;
  margin: 30px;
  border: #eca900 solid 3px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 #eca900;
  position: relative;
}
.box-img{
  width: 300px;
  height: 350px;
  position: relative;
}
.box-img img{
  width: 100%;
  height: 100%;
  object-fit: cover;
  /*border: 3px solid #eca900;*/


}
.name-pers{
  height: 50px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  color: #084525;
}
.name{
  font-size: 23px;
  color: #eca900;
}
.absolut{
  width: 35px;
  height: 350px;
  position: absolute;
  background-color:orange;
  right: -37px;
  bottom:-2px;
  border-top-right-radius: 15px;
  border-bottom-right-radius: 15px;
}
.text-vertical{
  width: 100%;
  height: 100%;
  writing-mode: vertical-lr;
  text-orientation: upright;
}
</style>