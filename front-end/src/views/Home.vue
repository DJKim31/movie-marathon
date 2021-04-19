<template>
  <div class="home">
    <h1>Welcome to the Movie Marathon Page!</h1>
    <p>You know what? One of fastest ways to improve your English is watching a movie in English. Still don't know what you can watch?</p>
    <p><strong>Then join this page!</strong></p>
    <p>Use <strong>"Find"</strong> to search for random movies depending on release periods. Or Use <strong>"Add"</strong> to add a new movie you want to watch later.</p>
    <p>Please <strong>"Login"</strong> to create a favorite list or write a movie review for others.</p>


    <div class="movies">
    <div v-for="movie in filteredMovies" :key="movie.id">
      <div class="movieImg">
        <img :src="movie.image">
      </div>
    </div>
  </div>
</div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data() {
    return {
      filteredMovies: []
    }
  },
  created() {
    this.earlyMovies()
  },
  components: {

  },
  methods: {
    earlyMovies () {
      let movie = this.$root.$data.Movies
      //console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; i += 25) {
        this.filteredMovies.push(movie[i])

      }


    },
  }
}
</script>


<style scoped>
  .home h1 {
    font-style: italic;
    color: black;
    font-size: 50px;
  }

  p {
    font-size: 20px;
    color: black;
  }
  .movies {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    margin-bottom: 50px;
    padding-top:50px

  }
  .movieImg {

  }
</style>
