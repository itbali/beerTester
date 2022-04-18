<template>

  <Loader v-if="loadingUser"/>
  <div v-else class="profileContainer">
    <n-h2>Profile:</n-h2>
<!--    Profile coontainer-->
      <div class="photoContainer">
        <n-image class="photoContainer__photo" :src="userProfile.avatar" alt="123" fallback-src="	https://vk.com/images/camera_400.png"/>
      </div>

      <table class="infoContainer">
        <n-tr><tc>name:</tc>{{ userProfile.first_name }} {{ userProfile.last_name }}</n-tr>
        <n-tr><tc>age:</tc>
          <tc>{{ countAge }}</tc></n-tr>
        <n-tr>
          <tc> employment:</tc> <tc> {{ userProfile.employment.title }} </tc></n-tr>
      </table>
    </div>
</template>

<script>
import Loader from '@/components/Loader'

export default {
  name: 'Profile',
  props: ['userProfile', 'loadingUser'],
  computed: {
    // counter of current age
    countAge() {
      let n = new Date(),
          b = new Date(this.userProfile.date_of_birth),
          age = n.getFullYear() - b.getFullYear();
      return n.setFullYear(1970) < b.setFullYear(1970) ? age - 1 : age;

    },
  },
  components: {
    Loader,
  },
}
</script>

<style scoped>
.profileContainer{
  width: 50vw;
  display: flex;
  margin: 20px;
  }

.photoContainer{
  width: 200px;
  height: 200px;
  margin: auto;
  }

.photoContainer__photo{
  width: 200px;
  height: 200px;
  object-fit: cover;
  border: 1px solid;
  border-radius: 50%;
  }

.infoContainer {
  margin-top: 20px;
  }

.infoContainer tr{
  display: flex;
  justify-content: space-between;
  }
.infoContainer tc{
  padding: 10px;
  }
@media (max-width: 1000px){
  .profileContainer{
    width: 60vw;
    }
  }

@media (max-width: 800px) {
  .profileContainer{
    width: 100%;
    flex-direction: column;
    position: relative;
    }
  .profileContainer::after{
    content: '';
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 1px;
    background: radial-gradient(ellipse at top,#ddd 0%,rgba(255,255,255,0) 70%);
    }
  }
</style>
