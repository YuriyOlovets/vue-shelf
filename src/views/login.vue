<template>
  <div v-if="Language" class="wrapper">
    <div class="header">
      <h3 class="sign-in" style="color: #008c8c">Вхід</h3>
      <a @click="toRegister">
      <div class="button">
        Реєстрація
      </div></a>
    </div>
    <div>
        <input v-model="login" class="user-input" type="text" name="name" id="name" placeholder="Логін"  />
        <input v-model="password" type="password" name="name" id="name" placeholder="Пароль" />
        <button @click="setLogin">Увійти</button>
      </div>



  </div>

  <div v-else class="wrapper">
    <div class="header">
      <h3 class="sign-in" style="color: #008c8c">Sign in</h3>
      <a @click="toRegister">
        <div class="button">
          Register
        </div></a>
    </div>
    <div>
      <input v-model="login" class="user-input" type="text" name="name" id="name" placeholder="Login"  />
      <input v-model="password" type="password" name="name" id="name" placeholder="password" />
      <button @click="setLogin">Sign in</button>
    </div>



  </div>

</template>

<script>
import $ from 'jquery'
export default {
  name: "Login",
  data() {
    return {
      login: '',
      password: '',
    }
  },
  computed: {
    Language(){
      if (localStorage.getItem('language')==='en')
        return false
      else
        return true
    }

  },
  methods: {
    setLogin() {

      $.ajax({
        url: "https://smart-shelf.net/api/auth/token/login/",
        type: "POST",
        data: {
          username: this.login,
          password: this.password
        },
        success: (response) => {
          localStorage.setItem("auth_token", response.auth_token)
          this.$router.push({name: "Home"})
          location.reload();
        },
        error: (response) => {
          if (response.status === 400) {
            alert("Логин или пароль не верен")
          }
        }
      })
    },
    toRegister(){
      this.$router.push({name: "register"})
    }
  }
}
</script>

<style scoped>
@import url(https://fonts.googleapis.com/css?family=Roboto:400,300,500);
*, *:after, *:before {
  box-sizing: border-box;
}

html, body {
  background: #1a1f25;
  font-family: 'Roboto', sans-serif;
}

.clear {
  clear: both;
}

#man-people-user, #lock-locker {
  fill: white;
}

.wrapper {
  width: 300px;
  margin: 12% auto;
}

form {
  position: relative;
}

.clear {
  clear: both;
}

.sign-in {
  float: left;
  color: white;
  font-size: 1.3em;
}

.button {
  float: right;
  color: #7f8084;
  border: 1px solid #22272d;
  padding: 7px 15px;
  border-radius: 3px;
  font-size: 0.8em;
  cursor: pointer;
}

.button:hover {
  color: #d3d3d3;
}

.lock {
  position: absolute;
  width: 30px;
  height: 30px;
  margin-top: 10px;
  padding: 7px;
  left: 5px;
}
.lock::after {
  content: "";
  width: 1px;
  height: 30px;
  position: absolute;
  background: #22272d;
  top: 0px;
  left: 100%;
}

.user {
  position: absolute;
  width: 30px;
  height: 30px;
  margin-top: 10px;
  padding: 7px;
  left: 5px;
}
.user::after {
  content: "";
  width: 1px;
  height: 30px;
  position: absolute;
  background: #22272d;
  top: 0px;
  left: 100%;
}

input {
  width: 100%;
  padding: 5px;
  height: 40px;
  border-radius: 3px;
  margin: 5px 0;
  outline: none;
}

input[type="text"]:focus, input[type="password"]:focus {
  border: 1px solid white;
  box-shadow: none;
}

.user-input:focus .user {
  background: white !important;
}

input[type="text"] {
  background: transparent;
  border: 2px solid #22272d;
  padding-left: 45px;
  color: #e6b333;
}

input[type="password"] {
  background: transparent;
  border: 2px solid #22272d;
  padding-left: 45px;
  color: #e6b333;
}

input[type="submit"] {
  background: #e6b333;
  border: none;
  color: white;
  text-align: center;
  font-size: 0.8em;
  cursor: pointer;
}

input[type="radio"] {
  display: none;
}

.radio-check {
  width: 50px;
  height: 20px;
  border: 1px solid #22272d;
  border-radius: 30px;
  margin-top: 10px;
  float: left;
  text-align: center;
  padding: 4px 0;
  color: #e6b333;
  font-size: 0.65em;
  position: relative;
}
.radio-check label {
  margin: 0 2px;
  cursor: pointer;
}
.radio-check .switch-selection {
  display: block;
  position: absolute;
  width: 11px;
  height: 11px;
  border-radius: 50%;
  background: #babbbd;
  margin-top: -11px;
  margin-left: 11px;
  -webkit-transition: 0.2s ease-out;
  transition: 0.2s ease-out;
}

.radio-yes:checked ~ .switch-selection {
  margin-left: 25px !important;
}

.check-label {
  font-size: 0.8em;
  color: #7f8084;
  margin-top: 10px;
  float: left;
  padding: 3px 0;
  margin-left: 10px;
}

.forgot-label {
  font-size: 0.8em;
  color: #7f8084;
  margin-top: 10px;
  float: right;
  padding: 3px 0;
  cursor: pointer;
}
</style>
