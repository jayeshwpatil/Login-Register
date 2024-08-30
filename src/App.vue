<script setup>
import { ref } from 'vue'
import loginVue from "./components/login.vue";
import registerVue from "./components/register.vue";

const RegisterUserName = ref('');
const registerEmail = ref('');
const registerPassword = ref('');

const fetchData = (data) => {
  console.log("result is ", data)
  RegisterUserName.value = data.userName;
  registerEmail.value = data.email;
  registerPassword.value = data.password;

}
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-6 border-end">
        <loginVue :RegisterUserName="RegisterUserName" :registerEmail="registerEmail"
          :registerPassword="registerPassword"></loginVue>
      </div>
      <div class="col-sm-6">
        <registerVue @userAllDetails="fetchData"></registerVue>
      </div>

    </div>
  </div>


</template>

<style>
body {
  background: #dbe4e4 !important;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.headingSection {
  font-size: 20px;
  font-weight: bold;
  padding-bottom: 15px;
  border-bottom: 2px solid #000;
  margin-bottom: 25px;
}

.container {
  background-color: #fff;
  border-radius: 40px;
  box-shadow: 10px 10px 5px #666;
  ;
}

.smallFont {
  font-size: 12px;
}

.valid {
  border: 1px solid green !important;
  /* background: #fff url('../public/download.png') 97% 8px no-repeat !important;
  background-size: 20px 20px; */
}

.invalid {
  border: 1px solid red !important
}
</style>