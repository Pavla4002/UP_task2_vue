<template>
  <div>
    <my-header v-model:input-val2="inputVal3"  v-model:model-value2="selectedSort" :options2="sortOptions"  v-model:model-value4="selectedSort2" :options4="sortOptions2" v-model:model-value5="selectedSort3" :options5="sortOptions3" @change1="openR" @open2="openA"/>
    <my-information :showInfo="statusUser" :userA="objectAuthoUser" :favorite-mag1="favoriteMag2" :favorite-magl1="favoriteMagl2"/>
    <post-list :posts="filterCharacter" @choice="log" :show-button1="statusUser" @add="addFavorites" @showValue="showValue2"/>
<!--    :value-button2="valueButton"-->
<!--    addFavorites-->
    <my-dialog v-model:show="dialogVisible">
      <my-character :post="character" />
    </my-dialog>
  <my-dialog v-model:show="openRegistration">
    <my-registration @create="regUser"/>
  </my-dialog>
    <my-dialog v-model:show="openAuthorization">
      <my-authorization @find="authoUser"/>
    </my-dialog>
  </div>
</template>

<script>
import MyInformation from "@/components/UI/MyInformation";
import MyRegistration from "@/components/MyRegistration";
import MyCharacter from "@/components/MyCharacter";
import MyDialog from "@/components/UI/MyDialog";
import PostList from "@/components/PostList";
import MyHeader from "@/components/UI/MyHeader";
import MyAuthorization from "@/components/MyAuthorization";
export default {
  components: {
    PostList,
    MyHeader,
    MyDialog,
    MyCharacter,
    MyRegistration,
    MyAuthorization,
    MyInformation
  },

  data(){
    return{
      posts:[],
      character:'',
      dialogVisible:false,
      openRegistration:false,
      openAuthorization:false,
      statusUser:false,
      objectAuthoUser:{},
      inputVal3:'',
      selectedSort:'none',
      selectedSort2:'none',
      selectedSort3:'none',
      sortOptions:[
        {value:'name',name:'По имени'},
        {value:'name1',name:'По имени - убывание'},
        {value:'actor',name:'По имени актера'},
        {value:'actor1',name:'По имени актера - убывание'},
        {value:'patronus',name:'Патронус'},
        {value:'patronus1',name:'Патронус - убывание'},
      ],
      sortOptions2:[
        {value:'Gryffindor',name:'Gryffindor'},
        {value:'Slytherin',name:'Slytherin'},
        {value:'Ravenclaw',name:'Ravenclaw'},
        {value:'Hufflepuff',name:'Hufflepuff'},
      ],
      sortOptions3:[
        {value:'male',name:'male'},
        {value:'female',name:'female'},
      ],
      favoriteMag2:0,
      favoriteMagl2:0,
      arrFavorites:[],
      valueButton: 'Add to favorites',
    }
  },
  methods:{
    async fetchPosts(){
      try {
        const  res = await fetch('https://hp-api.onrender.com/api/characters');
        this.posts = await res.json();
        console.log(this.posts);
      } catch (e) {
        console.error(e);
      }
    },
    showValue2($event,post){
      if(this.arrFavorites.includes(post) && this.arrFavorites.length!==0){
        $event.target.innerText = 'Add to favorites'
      }else{
        $event.target.innerText = 'Remove from favorites'
      }
    },
    log(post){
      this.character = post;
      this.dialogVisible = !this.dialogVisible;
    },
    openR(){
      this.openRegistration = !this.openRegistration;
    },
    openA(){
      this.openAuthorization = !this.openAuthorization;
    },
    regUser(post){
      let key = Date.now();
      let regExpFamOtch = /[А-Я]\W+/;
      let regExpName = /[А-Я]\W*/;
      let regExpNum = /8\(\d{3}\)\d{3}-\d{2}-\d{2}/;
      if(post.fam.match(regExpFamOtch) && post.otch.match(regExpFamOtch) && post.name.match(regExpName) && post.number.match(regExpNum) && (post.ageUser>=10)){
        console.log('hi')
        const userInfo = {
          login:post.login,
          password:post.password,
          fam:post.fam,
          name:post.name,
          otch:post. otch,
          number:post. number,
          interesUser:post.interesUser,
          ageUser:post.ageUser,
          genUser:post.genUser,
        }
        localStorage.setItem(key.toString(), JSON.stringify(userInfo));
        this.openR();
      }else{
        alert('Вы нарушили запись информации')
      }
    },
    authoUser(user){
      let userAuto;
      for (let i=0; i<localStorage.length; i++) {
        const key = localStorage.key(i);
        const value = localStorage[key];
        let user1 = JSON.parse(value);
        if (user.login===user1.login && user.password===user1.password) {
          userAuto=user1;
          this.statusUser = !this.statusUser;
          this.objectAuthoUser ={  //Для авторизации
            name:user1.name,
            fam:user1.fam,
            otch:user1.otch,
          }
          break;
        }
      }

      if (!userAuto) {
        alert("не найден пользователь");
      }
      this.openAuthorization = !this.openAuthorization
    },
    addFavorites(post){
      if(this.arrFavorites.includes(post) && this.arrFavorites.length!==0){
        console.log(this.arrFavorites.includes(post))
        console.log(this.arrFavorites)
        this.arrFavorites= this.arrFavorites.filter(p => p.id!==post.id)
        if(post.wizard===true){
          this.favoriteMag2-=1
        }else{
          this.favoriteMagl2-=1
        }
        // console.log(this.arrFavorites)
      }else{
        this.favoriteMag2=0
        this.favoriteMagl2=0
        let count = 0
        if(this.arrFavorites.length!==0){
          this.arrFavorites.forEach(el => {if(el.id!==post.id){count+=1}})
        }else{
          this.arrFavorites.push(post);
          // valueButton2=this.valueButton
        }
        if(count===this.arrFavorites.length){
          this.arrFavorites.push(post)
        }
        for(let i =0; i<this.arrFavorites.length;i++){
          if(this.arrFavorites[i].wizard===true){
            this.favoriteMag2+=1
          }else{
            this.favoriteMagl2+=1
          }
        }
        // console.log($event.target)
        // console.log(valueButton2)
      }
  },
  },
  mounted() {
    this.fetchPosts();
  },
  computed:{
    sortedPost(){
      switch (this.selectedSort){
        case 'name':
          return [...this.posts].sort((p,q) => p['name']?.localeCompare(q['name']));

        case 'actor':
          return [...this.posts].sort((p,q) => p['actor']?.localeCompare(q['actor']));

        case 'patronus':
          return [...this.posts].sort((p,q) => p['patronus']?.localeCompare(q['patronus']));

        case 'name1':
          return [...this.posts].sort((p,q) => -1 * p['name']?.localeCompare(q['name']));

        case 'actor1':
          return [...this.posts].sort((p,q) => -1 * p['actor']?.localeCompare(q['actor']));

        case 'patronus1':
          return [...this.posts].sort((p,q) => -1 * p['patronus']?.localeCompare(q['patronus']));

        default:
          return [...this.posts].sort((p,q) => p[this.selectedSort]?.localeCompare(q[this.selectedSort]));
      }
    },
    searchPost(){
      return this.sortedPost.filter(post =>((post.name.toLowerCase()).includes(this.inputVal3.toLowerCase())) || ((post.actor.toLowerCase()).includes(this.inputVal3.toLowerCase())) || ((post.ancestry.toLowerCase()).includes(this.inputVal3.toLowerCase())));
    },
    filterPost(){
      if(this.selectedSort2!=='none'){
        console.log(this.selectedSort2);
      return this.searchPost.filter(post => post.house === this.selectedSort2 );
      }else{
        return this.sortedPost.filter(post =>((post.name.toLowerCase()).includes(this.inputVal3.toLowerCase())) || ((post.actor.toLowerCase()).includes(this.inputVal3.toLowerCase())) || ((post.ancestry.toLowerCase()).includes(this.inputVal3.toLowerCase())));
      }
    },
    filterCharacter(){
      if(this.selectedSort3!=='none'){
        return this. filterPost.filter(post => post.gender === this.selectedSort3 );
      }else if (this.selectedSort3==='none' && this.selectedSort2!=='none'){
        return this.searchPost.filter(post => post.house === this.selectedSort2 );
      }
      else{
        return this.sortedPost.filter(post =>((post.name.toLowerCase()).includes(this.inputVal3.toLowerCase())) || ((post.actor.toLowerCase()).includes(this.inputVal3.toLowerCase())) || ((post.ancestry.toLowerCase()).includes(this.inputVal3.toLowerCase())));
        }
      }
  }
}
</script>

<style scoped>

</style>