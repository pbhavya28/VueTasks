<!-- TASK 1
------
using vue to create a avenger filter app
----------------------------------------
 
use the data that was shared in the class with female avengers that had movies list.
 
create a hero filter app which filters the list of avengers with the few characters entered by the user.
 
optionally you can ask the user to filter on first name, title and movies.
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx  -->


<script setup>
import { ref, computed } from "vue";

const ladyAvengers = ref([
  {
    title: "Wasp",
    firstname: "Janet",
    lastname: "Van Dyne",
    movies: [
      { title: "Ant-Man", year: 2015 },
      { title: "Ant‑Man and the Wasp", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Scarlet Witch",
    firstname: "Wanda",
    lastname: "Maximoff",
    movies: [
      { title: "Captain America: The Winter Soldier", year: 2014 },
      { title: "Avengers: Age of Ultron", year: 2015 },
      { title: "Captain America: Civil War", year: 2016 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
      { title: "Doctor Strange in the Multiverse of Madness", year: 2022 },
    ],
  },
  {
    title: "Black Widow",
    firstname: "Natasha",
    lastname: "Romanoff",
    movies: [
      { title: "Iron Man 2", year: 2010 },
      { title: "Avengers", year: 2012 },
      { title: "Captain America: The Winter Soldier", year: 2014 },
      { title: "Avengers: Age of Ultron", year: 2015 },
      { title: "Captain America: Civil War", year: 2016 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Captain Marvel",
    firstname: "Carol",
    lastname: "Danvers",
    movies: [
      { title: "Captain Marvel", year: 2019 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Gamora",
    firstname: "Gamora Zen",
    lastname: "Whoberi Ben Titan",
    movies: [
      { title: "Guardians of the Galaxy", year: 2014 },
      { title: "Guardians of the Galaxy Vol. 2", year: 2017 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Shuri",
    firstname: "Shuri",
    lastname: "Princess",
    movies: [
      { title: "Black Panther", year: 2018 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
      { title: "Black Panther: Wakanda Forever", year: 2022 },
    ],
  },
]);

const search = ref("");

const items = computed(() => {
  const query = search.value.trim().toLowerCase();
  if (!query) return ladyAvengers.value;

  return ladyAvengers.value.filter((character) => {
    const nameMatch =
      character.title.toLowerCase().includes(query) ||
      character.firstname.toLowerCase().includes(query);

    const movieMatch = character.movies.some((movie) =>
      movie.title.toLowerCase().includes(query)
    );

    return nameMatch || movieMatch;
  });
});
</script>

<template>
  <div class="container">
    <div class="searchbox">
      <input v-model="search" placeholder="Enter Avenger..." />
    </div>

    <ul>
      <li v-for="(item, index) in items" :key="index">
        <!-- <strong>{{ item.firstname }} "{{ item.title }}"</strong> -->
         <h5>{{ item.title }}</h5>
         <h5>{{ item.firstname }}</h5>
         <h5>{{ item.lastname }}</h5>
        <ul>
          <li v-for="movie in item.movies" :key="movie.title">{{ movie.title }} ({{ movie.year }})</li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.searchbox {
  display: flex;
  flex-direction: row;
  margin-bottom: 20px;
}
h5:nth-last-of-type(1){
    margin-bottom: 15px;
}
h5:nth-last-of-type(3){
    margin-top: 20px;
}
</style>


