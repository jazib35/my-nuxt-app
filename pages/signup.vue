<template>
    <div class="container d-flex justify-content-center align-items-center vh-100">
      <div class="card p-4 shadow-lg" style="width: 100%; max-width: 400px;">
        <h3 class="text-center mb-4">Sign Up</h3>
        <form @submit.prevent="handleSignUp">
          <div class="mb-3">
            <label for="name" class="form-label">Full Name</label>
            <input v-model="name" type="text" class="form-control" id="name" required />
          </div>
          <div class="mb-3">
            <label for="email" class="form-label">Email address</label>
            <input v-model="email" type="email" class="form-control" id="email" required />
          </div>
          <div class="mb-3">
            <label for="password" class="form-label">Password</label>
            <input v-model="password" type="password" class="form-control" id="password" required />
          </div>
          <div class="mb-3">
            <label for="confirmPassword" class="form-label">Confirm Password</label>
            <input v-model="confirmPassword" type="password" class="form-control" id="confirmPassword" required />
          </div>
          <button type="submit" class="btn btn-success w-100">Sign Up</button>
        </form>
        <p class="text-center mt-3">
          Already have an account? <NuxtLink to="/login">Login</NuxtLink>
        </p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import { useRouter } from 'vue-router'
  
  const name = ref('')
  const email = ref('')
  const password = ref('')
  const confirmPassword = ref('')
  const router = useRouter()
  
  const handleSignUp = () => {
    if (password.value !== confirmPassword.value) {
      alert('Passwords do not match!')
      return
    }
  
    console.log('Name:', name.value)
    console.log('Email:', email.value)
    console.log('Password:', password.value)
  
    // Here, you can send user details to an API for sign-up
  
    // Redirect to home page after sign-up
    router.push('/')
  }
  </script>
  