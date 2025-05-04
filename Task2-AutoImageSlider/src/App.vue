<!-- TASK 2
------
using vue and bootstrap create an auto image slider
---------------------------------------------------
 
use the same data as task 1 create an automatic image slider with indicators to show number of heroes and the current displayed hero highlighted.
 
a wireframe is attached for your reference. -->

<template>
  <div class="container mt-5">

    <div
      id="heroCarousel"
      class="carousel slide"
      data-bs-ride="carousel"
      data-bs-interval="3000"
    >

      <div class="carousel-indicators">
        <button
          v-for="(hero, index) in ladyAvengers"
          :key="index"
          type="button"
          :data-bs-target="'#heroCarousel'"
          :data-bs-slide-to="index"
          :class="{'active': index === currentIndex}"
          :aria-current="index === currentIndex ? 'true' : 'false'"
          :aria-label="'Slide ' + (index + 1)"
        ></button>
      </div>


<div class="carousel-inner">
  <div
    v-for="(hero, index) in ladyAvengers"
    :key="index"
    :class="['carousel-item', { active: index === currentIndex }]"
  >
    <div class="p-4 bg-light rounded d-flex flex-column align-items-center">

      <h2 class="text-center mb-4">{{ hero.title }}</h2>


      <div class="row w-100 align-items-center">

        <div class="col-md-5 text-center mb-3 mb-md-0">
          <img
            :src="hero.image"
            :alt="hero.title"
            class="img-fluid rounded shadow"
            style="height: 400px; object-fit: cover;"
          />
        </div>


        <div class="col-md-7">
          <h4>{{ hero.firstname }} {{ hero.lastname }}</h4>
          <h6 class="mt-3">Movies:</h6>
          <ul class="list-unstyled">
            <li v-for="(movie, i) in hero.movies" :key="i">
              {{ movie.title }} ({{ movie.year }})
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</div>



      <button
        class="carousel-control-prev"
        type="button"
        data-bs-target="#heroCarousel"
        data-bs-slide="prev"
      >
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
      </button>
      <button
        class="carousel-control-next"
        type="button"
        data-bs-target="#heroCarousel"
        data-bs-slide="next"
      >
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const ladyAvengers = ref([
    {
      title: 'Wasp',
      firstname: 'Janet',
      lastname: 'Van Dyne',
      image: './images/wasp.jpeg',
      movies: [
        { title: 'Ant-Man', year: 2015 },
        { title: 'Ant‑Man and the Wasp', year: 2018 },
        { title: 'Avengers: Endgame', year: 2019 }
      ]
    },
    {
      title: 'Scarlet Witch',
      firstname: 'Wanda',
      lastname: 'Maximoff',
      image: './images/scarletwitch.jpg',
      movies: [
        { title: 'Captain America: The Winter Soldier', year: 2014 },
        { title: 'Avengers: Age of Ultron', year: 2015 },
        { title: 'Captain America: Civil War', year: 2016 },
        { title: 'Avengers: Infinity War', year: 2018 },
        { title: 'Avengers: Endgame', year: 2019 },
        { title: 'Doctor Strange in the Multiverse of Madness', year: 2022 }
      ]
    },
    {
      title: 'Black Widow',
      firstname: 'Natasha',
      lastname: 'Romanoff',
      image: './images/blackwidow.jpg',
      movies: [
        { title: 'Iron Man 2', year: 2010 },
        { title: 'Avengers', year: 2012 },
        { title: 'Captain America: The Winter Soldier', year: 2014 },
        { title: 'Avengers: Age of Ultron', year: 2015 },
        { title: 'Captain America: Civil War', year: 2016 },
        { title: 'Avengers: Infinity War', year: 2018 },
        { title: 'Avengers: Endgame', year: 2019 }
      ]
    },
    {
      title: 'Captain Marvel',
      firstname: 'Carol',
      lastname: 'Danvers',
      image: './images/captainmarvel.jpg',
      movies: [
        { title: 'Captain Marvel', year: 2019 },
        { title: 'Avengers: Endgame', year: 2019 }
      ]
    },
    {
      title: 'Gamora',
      firstname: 'Gamora Zen',
      lastname: 'Whoberi Ben Titan',
      image: './images/gamora.jpeg',
      movies: [
        { title: 'Guardians of the Galaxy', year: 2014 },
        { title: 'Guardians of the Galaxy Vol. 2', year: 2017 },
        { title: 'Avengers: Infinity War', year: 2018 },
        { title: 'Avengers: Endgame', year: 2019 }
      ]
    },
    {
      title: 'Shuri',
      firstname: 'Shuri',
      lastname: 'Princess',
      image: './images/shuri.jpg',
      movies: [
        { title: 'Black Panther', year: 2018 },
        { title: 'Avengers: Infinity War', year: 2018 },
        { title: 'Avengers: Endgame', year: 2019 },
        { title: 'Black Panther: Wakanda Forever', year: 2022 }
      ]
    }
  ])

const currentIndex = ref(0);
let intervalId = null;

onMounted(() => {
  intervalId = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % ladyAvengers.value.length;
  }, 3000);
});

onBeforeUnmount(() => {
  clearInterval(intervalId);
});
</script>

<style scoped>
.carousel-indicators button {
  background-color: #000;
  border-radius: 50%;
  width: 12px;
  height: 12px;
  margin: 0 4px;
  opacity: 0.5;
}

.carousel-indicators .active {
  background-color: #fff;
  opacity: 1;
}
</style>
