<template>
  <Loading v-if="$fetchState.pending" />
 <div v-else class="single-movie container">
    <NuxtLink class="button" to="/"> Back </NuxtLink>
    <div class="movie-info">
      <div class="movie-img">
        <img
          :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
          alt=""
        />
      </div>
      <div class="movie-content">
        <h1>Title: {{ movie.title }}</h1>
        <p class="movie-fact tagline">
          <span>Tagline:</span> "{{ movie.tagline }}"
        </p>
        <p class="movie-fact">
          <span>Released:</span>
          {{
            new Date(movie.release_date).toLocaleString('en-us', {
              month: 'long',
              day: 'numeric',
              year: 'numeric',
            })
          }}
        </p>
        <p class="movie-fact">
          <span>Duration:</span> {{ movie.runtime }} minutes
        </p>
        <p class="movie-fact">
          <span>Revenue:</span>
          {{
            movie.revenue.toLocaleString('en-us', {
              style: 'currency',
              currency: 'USD',
            })
          }}
        </p>
        <p class="movie-fact"><span>Overview:</span> {{ movie.overview }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "single-movie",
  data() {
    return {
      movie: null,
    };
  },
  async fetch() {
    await this.getSingleMovie();
  },
  fetchDelay: 1000,
  methods: {
    async getSingleMovie() {
      const data = this.$axios.get(
        `https://api.themoviedb.org/3/movie/${this.$route.params.moviesId}?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US`
      );
      const result = await data
      this.movie = result.data;
      console.log(this.movie)
    
    },
  },
};
</script>


<style scoped>
</style>