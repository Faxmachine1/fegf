<template>
  <div class="profile-page py-16 max-w-md mx-auto">
    <h1 class="text-3xl font-bold mb-8 text-slate-800">My profile</h1>
    <div v-if="user" class="p-4 border rounded font-semibold text-nowrap text-stone-700 space-y-4">
      <img :src="user.image" alt="Profile Image" class="absolute size-32 rounded-full end-1/4 lg:size-48">
      <p>Username: {{ user.username }}</p>
      <p>Name: {{ user.firstName }}</p>
      <p>Lastname: {{ user.lastName }}</p>
      <p>Gender: {{ user.gender }}</p>
      <p>Email: {{ user.email }}</p>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Profile',
  data() {
    return {
      user: null,
    };
  },
  created() {
    fetch('https://dummyjson.com/auth/me', {
      method: 'GET',
      headers: {
        'Authorization': 'Bearer ' + localStorage.getItem('token'),
      },
    })
      .then((response) => response.json())
      .then((data) => {
        if (data.message === 'Invalid/Expired Token!') {
          this.$router.push('/login');
        } else {
          this.user = data;
        }
      });
  },
};
</script>

<style scoped>
/* Дополнительные стили */
</style>