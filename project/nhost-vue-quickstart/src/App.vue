<script setup>
  import { ref, onMounted } from 'vue'
  import { nhost } from "./lib/nhost"

  const getMoviesQuery = `
    query {
      movies {
        id
        title
        genre
        rating
      }
    }
  `;

  const movies = ref([])
  async function getMovies() {
    const { data } = await nhost.graphql.request(getMoviesQuery)
    movies.value = data.movies
  }

  onMounted(() => {
    getMovies()
  })
</script>

<template>
  <div>
    <table>
      <tbody>
        <tr v-for="movie in movies" :key="movie.id">
          <td>{{ movie.title }}</td>
          <td>{{ movie.genre }}</td>
          <td>{{ movie.rating }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>