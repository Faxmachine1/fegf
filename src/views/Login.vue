<template>
    <div class="login-page py-16 max-w-md mx-auto">
      <div class="flex">
        <h1 class="text-xl font-bold mb-8">Authorization</h1>
        <p v-if="error" class="ml-20 text-red-500 font-bold text-nowrap text-lg w-1/2">{{ error }}</p>
      </div>
      <form @submit.prevent="login" class="ml-20">
        <div class="mb-4">
          <label for="username" class="block text-gray-700">Login</label>
          <input type="text" v-model="username" id="username" class="w-1/2 px-3 py-2">
        </div>
        <div class="mb-4">
          <label for="password" class="block text-gray-700">Password</label>
          <input type="password" v-model="password" id="password" class="w-1/2 px-3 py-2">
        </div>
        <button type="submit" class="ml-12 px-4 py-2 text-gray-700">Submit</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Login',
    data() {
      return {
        username: '',
        password: '',
        error: null,
      };
    },
    methods: {
      login() {
        fetch('https://dummyjson.com/auth/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            username: this.username,
            password: this.password,
          }),
        })
          .then((response) => response.json())
          .then((data) => {
            if (data.accessToken) {
              localStorage.setItem('token', data.accessToken);
              this.$router.push('/profile');
            } else {
              this.error = data.message;
            }
          });
      },
    },
  };
  </script>
  
  <style scoped>
  /* Дополнительные стили */
  </style>
  