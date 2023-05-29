<template>
    <div class="dialog" v-if="show" @click.stop="hideDialog">
      <div class="content-dialog" @click.stop>
        <slot></slot>
      </div>
    </div>
</template>

<script>
export default {
  props:{
    show:{
      type:Boolean,
      default:false
    }
  },
  methods:{
    hideDialog(){
      this.$emit('update:show',false)
    }
  }
}
</script>

<style scoped>
.dialog{
  top:0;
  bottom: 0;
  left: 0;
  right: 0;
  background: #02520262;
  position: fixed;
  display: flex;
}
.content-dialog{
  margin: auto;
  background: white;
  border-radius: 20px;
  box-shadow: 0 0 21px -7px lightslategray;
  border: 2px transparent solid;
  width: 700px;
  height: 400px;
  display: flex;
  flex-direction: column;
  padding: 30px;
}
</style>