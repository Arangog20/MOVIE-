<template>
  <section class="details" v-if="movie">
    <div class="back-botton">
      <router-link to="/" class="botton">←</router-link>
    </div>

    <div class="details-movie">
      <div class="title-movie">
        <h1>{{ movie.Title }}</h1>
      </div>
      <div class="movie-container">
        <p><span>Year:</span> {{ movie.Year }}</p>
        <p><span>Rated:</span> {{ movie.Rated }}</p>
        <p><span>Genre:</span> {{ movie.Genre }}</p>
        <p><span>Director:</span> {{ movie.Director }}</p>
        <p><span>Runtime:</span> {{ movie.Runtime }}</p>
      </div>
      <div class="plot-movie">
        <h2>Plot</h2>
        <p>{{ movie.Plot }}</p>
        <div class="mov">
          <p><span>Awards:</span> {{ movie.Awards }}</p>
          <p><span>Language:</span> {{ movie.Language }}</p>
          <p><span>Country:</span> {{ movie.Country }}</p>
          <p><span>Metascore:</span> {{ movie.Metascore }}</p>
        </div>
      </div>
    </div>

    <div class="img-movie">
      <img :src="movie.Poster" :alt="movie.Title" />
    </div>
  </section>
  <p v-else>Loading...</p>
</template>

<script setup lang="ts">
import HTTP from '@/api/client-http';
import type { Movie } from '@/model/movie.model';
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const movieId = route.params.id as string;

const movie = ref<Movie | null>(null);

onMounted(async () => {
  try {
    const response = await HTTP.get('', {
      params: {
        i: movieId,
      },
    });
    movie.value = response.data;
  } catch (error) {
    console.error("Error fetching movie details:", error);
  }
});
</script>

<style scoped lang="scss">

.details {
  display: flex;
  align-items: flex-start;
  background-color: #181818;
  color: #fff;
  padding: 2rem;
  font-family: 'Roboto', sans-serif;
  justify-content: center;
  align-items: center;
  height: 100vh;

  .back-botton {
    position: absolute;
    top: 1rem;
    left: 1rem;

    .botton {
      color: #fff;
      font-size: 1.5rem;
      text-decoration: none;
    }
  }

  .details-movie {
    max-width: 800px; 
  width: 100%; 
  padding: 2rem;
  background-color: #1f1f1f;
  border-radius: 10px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);

    .title-movie h1 {
      font-size: 3rem;
      margin-bottom: 1rem;
      color: #650b7c;
    }

    .movie-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  padding: 1rem;
  background-color: #2b2b2b;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);

  p {
    font-size: 1.2rem;
    color: #e0e0e0;
    position: relative;
    padding-left: 1.5rem;

    span {
      font-weight: bold;
      color: #650b7c;
      margin-right: 0.5rem;
    }

    &::before {
      content: '';
      position: absolute;
      left: 0;
      top: 50%;
      width: 1rem;
      height: 1px;
      background-color: #555;
      transform: translateY(-50%);
    }
  }

  p:not(:last-child) {
    border-bottom: 1px dashed #444;
    padding-bottom: 0.5rem;
    margin-bottom: 0.5rem;
  }
}
    .plot-movie {
      margin-top: 2rem;

      h2 {
        font-size: 2rem;
        margin-bottom: 1rem;
      }

      p {
        font-size: 1.2rem;
        line-height: 1.5;
        margin-bottom: 1.5rem;
      }

      .mov {
        display: flex;
        flex-wrap: wrap;
        gap: 1.5rem;

        p {
          font-size: 1.2rem;
          span {
            font-weight: bold;
            color: #650b7c;
          }
        }
      }
    }
  }

  .img-movie {
    width: 35%;
    display: flex;
    justify-content: flex-end;

    img {
      width: 100%;
      height: auto;
      border-radius: 10px;
      box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.5);
    }
  }
}
</style>