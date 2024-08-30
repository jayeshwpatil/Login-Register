<script setup>
import { ref, onBeforeMount } from 'vue'
const props = defineProps(['RegisterUserName', 'registerEmail', 'registerPassword'])

const loginEmail = ref(null)
const loginPassword = ref(null)
const loginSuccessful = ref(false)
const remPassword = ref(false)
const loginId = ref(null)
const setError = ref(false)

onBeforeMount(() => {
  if (localStorage.getItem('user')) {
    loginSuccessful.value = true
    loginId.value = localStorage.getItem('user')
  }
})

const loginAuthontication = () => {
  //console.log("first", !props.registerEmail, !props.registerPassword)
  if (props.registerEmail && props.registerPassword && loginEmail.value == props.registerEmail && loginPassword.value == props.registerPassword) {
    loginSuccessful.value = true
    loginId.value = props.RegisterUserName
    console.log("login successful")
    if (remPassword.value == true) {
      localStorage.setItem('user', props.RegisterUserName);
    }
    else {
      return
    }

  }
  else {
    console.log("Invalid Username Password")
    setError.value = true
    setTimeout(() => {
      setError.value = false
    }, 2000)
  }
}



const logout = () => {
  localStorage.removeItem('user');
  loginSuccessful.value = false
}

</script>

<template>

  <div class="p-5">
    <h1 class="headingSection text-end">Login</h1>
    <form v-if="!loginSuccessful" class="mb-3">
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">Email address</label>
        <input type="email" class="form-control" id="exampleInputEmail1" v-model="loginEmail">
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1" v-model="loginPassword">
      </div>
      <div class="mb-3 form-check">
        <input type="checkbox" v-model="remPassword" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">Remember password</label>
      </div>
      <button type="submit" class="btn btn-success form-control" @click.prevent="loginAuthontication">Login</button>

    </form>
    <div v-if="setError" class="alert alert-danger customAlertStyle" role="alert"><i
        class="bi bi-exclamation-triangle-fill"></i>
      Invalid username or Password</div>

    <blockquote v-if="loginSuccessful">
      <div class="d-flex justify-content-between mb-2">
        <h4 class="d-inline">Hi, {{ loginId }}</h4><a class="d-inline " @click.prevent="logout">Logout</a>
      </div>

      <p>This is a simple demo website built using VueJS Composition API to demonstrate the login and registration
        process. The website features a responsive layout with a registration form on the right side and a login form on
        the left side.</p>
      <p>Following Technologies Used for this project</p>
      <ul>
        <li>HTML, CSS, and JavaScript</li>
        <li>VueJS Composition API</li>
      </ul>

    </blockquote>
  </div>

</template>

<style scoped>
label {
  width: 100%;
}

.customAlertStyle {
  padding: 7px 10px;
  font-size: 12px;
  font-weight: bold;
}
</style>