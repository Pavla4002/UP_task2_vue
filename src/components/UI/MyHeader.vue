<template>
  <div class="header">
    <div class="content-header">
      <div class="logo-search-select">
        <div class="logo-box">
          <img src="../../assets/img/harry_logo.png" alt="logo">
        </div>
          <my-search :input-val1="inputVal2" @input="inputValue2"/>
        <div class="position-element">
          <span class="span-style">Sort</span>
          <my-select :model-value="modelValue2" @change="selectOption" :options="options2"/>
        </div>
       <div class="position-element">
         <span class="span-style">Filter house</span>
         <my-select :model-value="modelValue4" @change="selectOption2" :options="options4"/>
       </div>
        <div class="position-element">
          <span class="span-style">Filter gender</span>
          <my-select :model-value="modelValue5" @change="selectOption3" :options="options5"/>
        </div>

      </div>
     <div class="autho-reg">
       <my-button class="reg" @click="openR">Регистрация</my-button>
       <my-button @click="openAutho">Авторизация</my-button>
    </div>
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
import MySearch from "@/components/MySearch";
import MySelect from "@/components/MySelect";
export default {
  components:{
    MySearch,
    MySelect,
    MyButton
  },
props:{
  inputVal2:{
    type: String,
    default:'',
  },
  modelValue2:{
    type:String
  },
  options2:{
    type:Array,
    default: () => []
  },
  modelValue4:{
    type:String
  },
  options4:{
    type:Array,
    default: () => []
  },
  modelValue5:{
    type:String
  },
  options5:{
    type:Array,
    default: () => []
  },
  openReg:{
    type:Boolean,
    default:false
  },
  openAuthorization:{
    type:Boolean,
    default:false
  },
},
  methods:{
    inputValue2(event){
      this.$emit('update:inputVal2', event.target.value);
    },
    selectOption(e){
      this.$emit('update:modelValue2',e.target.value );
    },
    selectOption2(e){
      this.$emit('update:modelValue4',e.target.value );
    },
    selectOption3(e){
      this.$emit('update:modelValue5',e.target.value );
    },
    openR(){
      this.$emit('change1',this.openReg);
    },
    openAutho(){
      this.$emit('open2',this.openAuthorization);
    }
  }
}
</script>

<style scoped>
.header{
  width: 100%;
  height: 150px;
  background-color: #084525;
}
.logo-search-select{
  display: flex;
  justify-content: space-between;
  width: 1100px;
}
.logo-box{
  width: 200px;
  height: 100px;
}
.logo-box img{
  width: 170px;
  height: 170px;
}
.content-header{
  display: flex;
  justify-content: space-between;
  padding: 20px;
}
.span-style{
  color: #eca900;
  margin-bottom: 7px;
  font-size: 20px;
}
.position-element{
  display: flex;
  flex-direction: column;
}
.autho-reg{
  height: 80px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.reg{
  border: #eca900 solid 2px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 #eca900;
}
</style>