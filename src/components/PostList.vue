<template>
  <div class="list-post">
    <post-item v-for="post in posts" :post="post" :key="post.id" @choice="$emit('choice',post)" :show-button="showButton1" @add="$emit('add',post)" @showValue="$emit('showValue',$event,post)"/>
<!--    :value-button="valueButton2"-->
  </div>
<!--  @add="$emit('add',post)"-->
</template>


<script>
import PostItem from "@/components/PostItem";
export default {
  components: {
    PostItem,
  },
  props:{
    posts:{
      type: Array,
      required: true
    },
    showButton1:{
      type:Boolean,
      default:false
    },
   masFavorites1:{
     type:Array,
     default: () =>[]
    },
    valueButton2:{
      type:String,
      default:'Add to favorites'
    }
  },
}
</script>

<style scoped>
.list-post{
  width:80%;
  margin: 0 auto;
  display: flex;
  justify-content: start;
  flex-wrap: wrap;

}
</style>