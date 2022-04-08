<template>
  <navbar @new-user="fetchUserAndBeer"></navbar>
  <div class="info">
    <div v-if="!isUserLoading">
      <user-info :user="user"  class="user__info"></user-info>
    </div>
    <div v-else>Loading</div>
    <div class="beer__block">
      <div v-if="!isBeerLoading">
        <beer-info :beer="beer" class="beer__info"></beer-info>
        <my-button @click="fetchBeer" class="beer__btn">Сменить пиво</my-button>
      </div>
      <div v-else>Loading</div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar";
import UserInfo from "@/components/UserInfo";
import BeerInfo from "@/components/BeerInfo";
import MyButton from "@/components/UI/MyButton";
import axios from "axios";
export default {
  name: 'App',
  components: {
    MyButton,
    Navbar,
    UserInfo,
    BeerInfo
  },
  data() {
    return {
      user: {
        name: String,
        workPosition: String,
        age: String,
        photoUrl: String
      },
      beer: {
        brand: String,
        name: String,
        alcohol: String
      },
      isUserLoading: false,
      isBeerLoading: false
    }
  },
  methods: {
    async fetchUser() {
      try {
        this.isUserLoading = true
        const response = await axios.get('https://random-data-api.com/api/users/random_user')
        this.user.name = `${response.data.first_name} ${response.data.last_name}`
        this.user.workPosition = response.data.employment.title
        this.user.age = this.fullAge(response.data.date_of_birth)
        this.user.photoUrl = response.data.avatar
      } catch (e) {
        alert("Ошибка загрузки пользователя")
      } finally {
        this.isUserLoading = false
      }
    },
    async fetchBeer() {
      try {
        this.isBeerLoading = true
        const response = await axios.get('https://random-data-api.com/api/beer/random_beer')
        this.beer.brand = response.data.brand
        this.beer.name = response.data.name
        this.beer.alcohol = response.data.alcohol
      } catch (e) {
        alert("Ошибка загрузки пива")
      } finally {
        this.isBeerLoading = false
      }
    },
    fullAge(date) {
      date = date.split('-')
      const dateNow = [new Date().getFullYear(), new Date().getMonth() + 1, new Date().getDate()]
      return dateNow[1] == date[1] && dateNow[2] >= date[2] ? dateNow[0] - date[0] : dateNow[1] > date[1] ? dateNow[0] - date[0] : dateNow[0] - date[0] - 1
    },
    fetchUserAndBeer() {
      this.fetchUser()
      this.fetchBeer()
    }
  },
  mounted() {
    this.fetchUser()
    this.fetchBeer()
  }
}
</script>

<style lang="scss">
@import 'src/styles/_variables.scss';
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: $yellow;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: $brown;
}
.info {
  display: flex;
  justify-content: center;
  .user__info {
    margin: 10px 5vw;
  }
  .beer__block {
    width: 300px;
  }
  .beer__info {
    margin: 10px;
  }
  .beer__btn {
    display: flex;
    margin: 10px auto;
    width: 120px;
  }
}
@media screen and (max-width: 600px) {
.info {
  flex-direction: column;
  align-items: center;
  .user__info {
    margin: 10px;
  }
}
}
</style>
