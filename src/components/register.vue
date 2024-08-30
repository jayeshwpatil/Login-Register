<script setup>
import { computed, ref } from 'vue'

const smallLetter = ref("abcdefghijklmnopqrstuvwxyz");
const capsLetter = ref("ABCDEFGHIJKLMNOPQRSTUVWXYZ");
const numbers = ref("1234567890");
const specialChar = ref("!@#$%^&*()");

let autoGeneratePassword = ref('');
// let y = [smallLetter, capsLetter, numbers, specialChar];
let y = [smallLetter, numbers, specialChar, capsLetter, smallLetter, specialChar, capsLetter, numbers];
let z = ""
const generatePassword = () => {
  for (let x = 0; x < y.length; x++) {
    // z = z + y[x].value.charAt(Math.floor(Math.random() * y[x].value.length)) + y[x].value.charAt(Math.floor(Math.random() * y[x].value.length))
    z = z + y[x].value.charAt(Math.floor(Math.random() * y[x].value.length))
  }
  formData.value.password = z;
  z = "";                               //for second time password generation clear first value
}



const formData = ref({
  userName: '',
  email: '',
  password: ''
})
const formSuccess = ref(null)
const isValidName = computed(() => /^[a-z]+$/.test(formData.value.userName))
const isValidEmail = computed(() => /[A-Za-z0-9\._%+\-]+@[A-Za-z0-9\.\-]+\.[A-Za-z]{2,}/.test(formData.value.email))
const isValidPassword = computed(() => /^(?=.*?[A-Z])(?=.*?[a-z])(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).{8,}$/.test(formData.value.password))

function submitedRegisterData() {
  if (isValidName.value && isValidEmail.value && isValidPassword.value) {
    console.log("user registered successfully")
    console.log(`user name : ${formData.value.userName}  email : ${formData.value.email}  password : ${formData.value.password}`)


    setTimeout(function () {
      //formSuccess.value = null;
      // Clear form data after successful registration
      formData.value.userName = '';
      formData.value.email = '';
      formData.value.password = '';
    }, 1500);

    formSuccess.value = true
    setTimeout(function () {
      formSuccess.value = null
    }, 1500);

    return formData.value
  }
  else {
    console.log("enter proper data")

    formSuccess.value = false
    setTimeout(function () {
      formSuccess.value = null
    }, 1500);
  }
}

</script>

<template>
  <div class="p-5">
    <h1 class="headingSection text-end">Register </h1>
    <form>
      <div class="mb-3">
        <label for="exampleUserName2" class="form-label">User Name</label>
        <input type="text" :class="{ 'valid': isValidName }" class="form-control" id="exampleUserName2"
          v-model.trim="formData.userName" required>
      </div>
      <div class="mb-3">
        <label for="exampleInputEmail2" class="form-label">Email address</label>
        <input type="email" :class="{ 'valid': isValidEmail }" class="form-control" id="exampleInputEmail2"
          v-model="formData.email" required>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword2" class="form-label">Password</label>
        <input type="text" :class="{ 'valid': isValidPassword }" class="form-control d-inline w-50"
          id="exampleInputPassword2" v-model="formData.password" required>
        <span class="mx-3 d-inline">or</span>
        <button type="button" class="btn btn-sm btn-dark d-inline" @click="generatePassword">Generate Password</button>
      </div>

      <!-- <p class="smallFont mt-2 ">"Your password must be at least 8 characters long and contain at least one uppercase
          letter, one lowercase
          letter, a number, and a special character."</p> -->


      <button type="submit" @click.prevent="$emit('userAllDetails', submitedRegisterData())"
        class="btn btn-success form-control mb-3">Register</button>
    </form>
    <div v-if="formSuccess == false" class="alert alert-danger customAlertStyle" role="alert"><i
        class="bi bi-exclamation-triangle-fill"></i> Please Enter Valid Details</div>
    <div v-if="formSuccess == true" class="alert alert-success customAlertStyle" role="alert"><i
        class="bi bi-check-circle"></i> Account Register Successfully</div>
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