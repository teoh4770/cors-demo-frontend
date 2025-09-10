<script setup lang="ts">
  import axios from 'axios'
  import { onMounted, ref } from 'vue'

  const message = ref('Loading');

  onMounted(async () => {
    try {
      // Make a get request to our Laravel API endpoint
      const response = await axios.get('http://localhost:8000/api/greeting');

      // Update the message with the data from the API
      message.value = response.data.message;
    } catch (e) {
      console.error('There was an error fetching the data:', e);
      message.value = 'Failed to load message from API. Is the Laravel server running?';
    }
  });

</script>

<template>
  <main>
    <h1>Vue + Laravel Demo</h1>
    <p>
      Message from API: <strong>{{ message }}</strong>
    </p>
  </main>
</template>

<style scoped>
main {
  font-family: sans-serif;
  text-align: center;
  margin-top: 50px;
}
strong {
  color: #42b983; /* Vue Green */
}
</style>
