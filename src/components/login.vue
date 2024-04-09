<script setup>
import { ref, computed } from "vue";

const formData = ref({
  email: "",
  password: "",
});

const isEmailValid = computed(() =>
  /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email)
);
const isPasswordValid = computed(() => formData.value.password.length >= 8);

const isFormValid = computed(() => isEmailValid.value && isPasswordValid.value);

const loginUser = () => {
  if (isFormValid.value) {
    // Perform simple authentication (replace with actual login logic)
    if (formData.value.email === "user@example.com" && formData.value.password === "password") {
      console.log("Login successful!");
      // Redirect to another page or perform actions upon successful login
    } else {
      console.log("Invalid credentials. Please try again.");
    }
  } else {
    console.log("Form is invalid. Please check the fields.");
  }
};
</script>

<template>
  <div class="login-page">
    <h2>Login</h2>
    <div class="login-container">
      <form @submit.prevent="loginUser" class="custom-form">
        <div class="form-group">
          <label for="email">Email:</label>
          <input v-model="formData.email" type="email" id="email" />
          <span v-if="!isEmailValid" class="error">Please enter a valid email address</span>
        </div>

        <div class="form-group">
          <label for="password">Password:</label>
          <input v-model="formData.password" type="password" id="password" />
          <span v-if="!isPasswordValid" class="error">Password must be at least 8 characters</span>
        </div>

        <button type="submit" :disabled="!isFormValid" class="submit-button">
          <b>Login</b>
        </button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  flex-direction: column; /* Stack children vertically */
}

.login-container {
  max-width: 400px;
  width: 100%;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  margin-top: 20px; /* Add space between title and form */
  background: #dbeefc;
}

.custom-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}

input {
  width: 95%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.error {
  color: #e74c3c;
  font-size: 14px;
  margin-top: 5px;
}

.submit-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #3498db;
  color: #0a0a0a;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.submit-button:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}
</style>
