<script setup>
const props = defineProps({
  hero: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div v-if="hero" class="container">
        <h1> {{ hero.title }}</h1>
        <div class="class-for-img-movies">
            <img :src="hero.image" :alt="hero.title" class="img-fluid" />
            <ul>
                <li class="movies-text">Movies</li>
                <li v-for="movie in hero.movies" :key="hero.title">{{ movie.title }} ({{ movie.year }})</li>
            </ul>
        </div>
  </div>
</template>

  
  <style scoped>
  
  img {
    height: 400px;
    width: 30%;
    object-fit: cover;
  }
  .container{
    display: flex;
    flex-direction: column;
    gap:15px;
  }
  .class-for-img-movies{
    display: flex;
    flex-direction: row;
    gap:15px;
  }
  li{
    text-align: left;
  }
  h1{
    display: inline-block;
    background-color: black;
    color: antiquewhite;
  }
  ul{
    display: block;
    background-color: gray;
    color: aliceblue;
    width: 100%;
    height: 400px;
  }
  .movies-text{
    font-size: 30px;
    mask-type: alpha;
    color: greenyellow;
    margin-bottom: 10px;
  }
  </style>
  