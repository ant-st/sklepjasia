<script>
import {password as correctPassword} from "@/passwords";
export default {
  name: "TheLogger",
  props: {
    loggedIn: Boolean
  },
  data() {
    return {
      password: '',
      wrongPasswordClass: false
    }
  },
  methods: {
    handleLogOut() {
      this.$emit('logout')
    },
    handleLogIn() {
      if (this.password === correctPassword) {
        this.$emit('login');
        this.password = '';
      }
      else {
        this.password = '';
        this.wrongPasswordClass = true;
        setTimeout(() => this.wrongPasswordClass = false, 2000)
      }
    }
  }
}
</script>

<template>
  <div id="the-logger">
    <div v-if="!loggedIn" id="login-field">
      <input type="password" v-model="password" :class="{wrongPasswordClass}" placeholder="Podaj hasło"/>
      <button class="login-button" @click="handleLogIn">ZALOGUJ</button>
    </div>
    <button class="login-button" v-else @click="handleLogOut">WYLOGUJ</button>
  </div>
</template>

<style scoped>

#the-logger {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 350px;
  text-align: center;
  margin: 5px auto;
  z-index: 2;
}

#login-field {
  display: flex;
  justify-content: space-evenly;
}

#login-field input {
  width: 40%;
  color: #ebebeb;
  background: none;
  border: 2px solid #2c3e50;
  border-radius: 10px;

  transition: border 0.2s linear;
}

#login-field .wrongPasswordClass {
  border: 2px red solid;
}

.login-button {
  width: 40%;
  padding: 10px;
}


@media screen and (max-width:1000px) {
  #the-logger {
    width: 220px;
  }
  @media screen and (max-width: 650px) {
    #the-logger {
      position: relative;
      top: auto
    }
  }
}

</style>