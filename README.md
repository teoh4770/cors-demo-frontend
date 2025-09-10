Let's create the app that will talk to our API.

1. Create a New Vue Project

In a new terminal window (keep your Laravel server running!), navigate to your main development folder and run:

```Bash

# This will guide you through creating a new Vue 3 project
npm create vue@latest
When prompted, you can name it my-vue-app and choose the default settings (No to everything is fine for this simple example).
```
2. Install Dependencies

Navigate into your new Vue project and install the dependencies, plus axios for making HTTP requests.

```Bash

cd my-vue-app
npm install
npm install axios
```

3. Create the Vue Component

Open src/App.vue and replace its entire content with the following code. This code will fetch the message from our Laravel API when the component is created and display it.

```Vue
<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

// A reactive variable to store the message from the API
const message = ref('Loading...');

// This function will be called when the component is mounted
onMounted(async () => {
  try {
    // Make a GET request to our Laravel API endpoint
    const response = await axios.get('http://localhost:8080/api/greeting');

    // Update the message with the data from the API
    message.value = response.data.message;

  } catch (error) {
    // If an error occurs (like a CORS error or network issue), display it
    console.error("There was an error fetching the data:", error);
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
```