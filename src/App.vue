<template>
  <n-h1>Beer selector</n-h1>
  <hr>
  <div class="mainContainer">
  <Profile :userProfile='userProfile' :loadingUser="loadingUser"/>
  <Beer :randomBeer="randomBeer" :loadingBeer="loadingBeer" @reloadBeer="reloadBeer"/>
  </div>
  <hr>
</template>

<script>
import Profile from '@/components/Profile'
import Beer from '@/components/Beer'
import Loader from '@/components/Loader'

export default {
  data() {
    return {
      userProfile: {},
      randomBeer: {},
      loadingUser: true,
      loadingBeer: true,
    }
  },
  mounted() {
    fetch('https://random-data-api.com/api/users/random_user')
        .then(response => response.json())
        .then(json => {
          this.userProfile = json
          console.log(json)
          this.loadingUser = false
        });
    fetch('https://random-data-api.com/api/beer/random_beer')
        .then(response => response.json())
        .then(json => {
          this.randomBeer = json
          this.loadingBeer = false
        })

  },
  methods: {
    reloadBeer(){
      this.loadingBeer = true
      fetch('https://random-data-api.com/api/beer/random_beer')
          .then(response => response.json())
          .then(json => {
            this.randomBeer = json
            this.loadingBeer = false
          })
    }
  },
  components: {
    Profile, Loader, Beer
  }
}
</script>

<style>
.mainContainer{
  display: flex;
  }
@media (max-width: 800px) {
  .mainContainer{
    flex-direction: column;
    margin:0 20vw ;
    }
  }

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  }
</style>
