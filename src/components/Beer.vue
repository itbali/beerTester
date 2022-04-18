<template>
  <div class="beerContainer">
    <Loader v-if="loadingBeer"/>
    <div v-else>
      <div>
        <n-h2> Beer for today</n-h2>
        <table class="beerContainer__table">
          <thead>
          <tr>
            <th>brand</th>
            <th>name</th>
            <th>style</th>
            <th>alcohol</th>
          </tr>
          </thead>
          <tbody>
          <tr>
            <td>{{ randomBeer.brand }}</td>
            <td>{{ randomBeer.name }}</td>
            <td>{{ randomBeer.style }}</td>
            <td>{{ randomBeer.alcohol }}</td>
          </tr>
          </tbody>
        </table>
      </div>
      <br>
      <n-button strong secondary round @click="$emit('reloadBeer')">Reload</n-button>
      <br>
    </div>
  </div>
</template>

<script>
import Loader from '@/components/Loader'

export default {
  props: ['randomBeer', 'loadingBeer'],
  components: {
    Loader,
  },
}
</script>

<style scoped>
.beerContainer {
  position: relative;
  width: 50vw;
  display: flex;
  flex-direction: column;
  margin: 20px;
  }

.beerContainer::before {
  content: '';
  position: absolute;
  left: -10px;
  top: 0;
  width: 1px;
  height: 100%;
  background: radial-gradient(ellipse at top, #969191 0%, rgba(169, 164, 164, 0) 70%);
  }

.beerContainer__table{
  width: 100%;
  }

@media (max-width: 1000px){
  .beerContainer{
    width: 40vw;
    }
  }

@media (max-width: 800px) {
  .beerContainer {
    width: 100%;
    height: 120px;
    }
  .beerContainer::before {
    content: none;
    }
  }
</style>
