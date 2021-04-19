<template>
  <div id="app">
    <div class="user" v-if="this.$root.$data.user != null">
      <h2> Logged in as {{user.firstName}} {{user.lastName}} <br> <a @click="logout">Log Out</a></h2>
    </div>
    <div id="nav">
      <router-link class="router" to="/">Home </router-link>
      <div v-if="this.$root.$data.user != null">
      <router-link class="router" to="/Favorites">Favorites </router-link>
    </div>
      <router-link class="router" to="/Find">Find </router-link>
      <router-link class="router" to="/Add">Add </router-link>
      <router-link class="router" to="/Login">Login</router-link>
    </div>
    <router-view/>
  <!--<p> {{GetFirstItem}} </p>-->



  <div class="github-footer"><a href='https://github.com/DJKim31/movie-marathon.git'>DJ's repo 20 hours</a></div>
  </div>

</template>



<script>
import axios from 'axios';
export default {
  async created() {
   try {
     let response = await axios.get('/api/users');
     this.$root.$data.user = response.data.user;
   } catch (error) {
     this.$root.$data.user = null;
   }
 },

  computed: {

    numCartItems () {
      const numItems = this.$root.$data.numItems
      return numItems
    },
    GetFirstItem () {
    return this.$root.$data.Movies[0]
    },
    user() {
    return this.$root.$data.user;
  },

  },
  methods: {
    async logout() {
  try {
    await axios.delete("/api/users");
    this.$root.$data.user = null;
  } catch (error) {
    this.$root.$data.user = null;
  }
},
  }

  }

</script>

<style>
body {
  background-image: url("../images/movie.jpg");
}

.github-footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: #F0F8FF;
  color: white;
  text-align: center;
  font-size: auto;
}

h2 {
  font-size: 16px;
  float: right;
}

.router {
  margin-right: 5px;
  margin-left: 5px;
}

#app {
  font-family: Impact, fantasy;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 10px;
  font-size: 40px;
  padding-top: 50px;
  display: flex;
  flex-direction: row;
  margin: 20px;
  justify-content: space-evenly;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}
a {
  text-decoration: underline;
}

#nav a.router-link-exact-active {
  color: purple;
}

@media only screen and (max-width:401px) {
  #nav {
    font-size: 20px;
  }

}
</style>
