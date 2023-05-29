<template>
  <div class="box-autho">
    <span>Авторизаця</span>
    <div class="login">
      <label for="login">Введите логин</label>
      <input type="text" id="login" v-model="user.login">
    </div>
    <div class="password">
      <label for="password">Введите пароль</label>
      <input type="text" id="password" v-model="user.password">
    </div>
    <my-button class="btn" @click="autho">Авторизоваться</my-button>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  components: {MyButton},
    data(){
      return{
      user:{
        login:'',
        password:'',
      }
      }
    },
    methods:{
      autho(){
        this.$emit('find',this.user);
      }
    }
}
</script>

<style scoped>
.box-autho{
  padding-top: 50px;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.login, .password{
  display: flex;
  flex-direction: column;
  margin-top: 30px;
  width: 80%;
}
.btn{
  margin-top: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 200px;
  background-color: #084525;
  color: white;
}

</style>