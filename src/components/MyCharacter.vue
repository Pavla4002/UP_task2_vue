<template>
  <div class="big-card-personage">
    <div class="photo-reps">
      <img src="../assets/img/Нет_фото.png" alt="" class="with-img" v-if="post.image === '' ">
      <img :src="post.image" alt="" v-else>
    </div>
    <div class="information-pers-block">
      <ul>
        <li>id: {{post.id}}</li>
        <li>name: {{post.name}}</li>
        <li>alternate_names: {{post.alternate_names[0]}}</li>
        <li>{{post.alternate_names[1]}}</li>
      </ul>
      <div class="box-2-info">
        <ul>
          <li>Species: {{post.species}}</li>
          <li>gender: {{post.gender}}</li>
          <li>house: {{post.house}}</li>
          <li>dateOfBirth: {{post.dateOfBirth}}</li>
          <li>yearOfBirth: {{post.yearOfBirth}}</li>
          <li>wizard: {{post.wizard}}</li>
        </ul>
        <ul>
          <li>ancestry: {{post.ancestry}}</li>
          <li>eyeColour: {{post.eyeColour}}</li>
          <li>hairColour: {{post.hairColour}}</li>
          <li>patronus: {{post.patronus}}</li>
          <li>hogwartsStudent: {{post.hogwartsStudent}}</li>
          <li>hogwartsStaff: {{post.hogwartsStaff}}</li>
          <li>actor: {{post.actor}}</li>
        </ul>
      </div>
      <div class="box-3-info">
        <ul>
          <li>alternate_actors: {{post.alternate_actors[0]}}</li>
          <li>alive: {{post.alive}}</li>
          <li>wood: {{post.wand.wood}}</li>
          <li>core: {{post.wand.core}}</li>
          <li>length: {{post.wand.length}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    post:{
      type:Object,
      required:true
    }
  },
}
</script>

<style scoped>
ul{
  list-style: none;
}
.big-card-personage{
  padding: 10px;
  display: flex;
  justify-content: start;
}
.information-pers-block{
  display: flex;
  flex-direction: column;
}
.box-2-info{
  display: flex;
  justify-content: space-between;
}
.photo-reps{
  width:300px;
  height: 380px;
}
.photo-reps img{
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>