<template>
  <div class="registration" >
    <label for="login">Введите логин</label>
    <input type="text" id="login" v-model="post.login">
    <label for="password">Введите пароль</label>
    <input type="text" id="password" v-model="post.password">
    <div class="blocks-input">
      <div class="block1">
        <div class="margin column">
          <label for="fam">Введите фамилию</label>
          <input type="text" id="fam" v-model="post.fam">
        </div>
        <div class="margin column">
          <label for="name">Введите имя</label>
          <input type="text" id="name" v-model="post.name">
        </div>
        <div class="margin column">
          <label for="otch">Введите отчество</label>
          <input type="text" id="otch" v-model="post.otch">
        </div>
        <div class="margin column">
          <label for="number">Введите номер телефона</label>
          <input type="text" id="number" v-model="post.number">
        </div>
      </div>
      <div class="block2">
        <div class="check">
          <span>Любимый факультет в Хогвартсе: </span>
          <div class="margin">
            <input type="checkbox" id="hogv" v-model="post.interesUser" value="Гриффиндор">
            <label for="hogv">Гриффиндор</label>
          </div>
          <div class="margin">
            <input type="checkbox" id="kog" v-model="post.interesUser" value="Когтевран">
            <label for="kog">Когтевран</label>
          </div>
          <div class="margin">
            <input type="checkbox" id="puf" value="Пуффендуй"  v-model="post.interesUser">
            <label for="puf">Пуффендуй</label>
          </div>
          <div class="margin">
            <input type="checkbox" id="sliz" v-model="post.interesUser" value="Слизерин">
            <label for="sliz">Слизерин</label>
          </div>
        </div>
        <label for="age" class="margin">Ваш возраст: </label>
        <input type="text" id="age" v-model="post.ageUser">
        <div class="gender">
          <div class="margin">
            <label for="male">Мужской</label>
            <input type="radio" id="male" name="gen" value="Мужской" v-model="post.genUser">
          </div>
          <div class="margin">
            <label for="female">Женский</label>
            <input type="radio" id="female" name="gen" value="Женский"  v-model="post.genUser">
          </div>

        </div>
      </div>
    </div>
    <div class="button-box">
      <my-button class="btn" @click="regUser">Регистрация</my-button>
    </div>

  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  components: {
    MyButton
  },
  data(){
    return{
      post:{
        login:'',
        password:'',
        fam:'',
        name:'',
        otch:'',
        number:'',
        interesUser:[],
        ageUser:'',
        genUser:'',
      }
    }
  },
  methods:{
    regUser(){
      this.$emit('create', this.post);
    }
  }

}
</script>

<style scoped>
.registration{
  display: flex;
  flex-direction: column;
}
.blocks-input{
  display: flex;
  justify-content: space-between;
}
.block1, .block2{
  margin-top: 20px;
  width: 330px;
  display: flex;
  flex-direction: column;
}
.check{
  display: flex;
  flex-direction: column;
}
.margin{
  margin: 5px;
}
.column{
  display: flex;
  flex-direction: column;
}
.button-box{
  margin-top: 20px;
  width: 100%;
  display: flex;
  justify-content: center;
}
.btn{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 200px;
  background-color: #084525;
  color: white;
}
</style>