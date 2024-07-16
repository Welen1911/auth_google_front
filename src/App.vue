<script setup>
import axios from 'axios';
import { onBeforeMount, onMounted, ref } from 'vue';

onBeforeMount(async () => {


  const query = new URLSearchParams(location.search);
  const authCode = query.get('code');

  if (authCode) {
    console.log(authCode);
    try {
      const { data } = await axios.post('http://localhost/api/login/callback', {
        code: authCode
      });

      console.log(data);

    } catch (e) {
      console.error(e);
    }
  }



});


const link = ref("");

onMounted(async () => {
  try {
    const { data } = await axios.get('http://localhost/api/login');

    console.log(data.url);

    link.value = data.url;

  } catch (e) {

  }
});
</script>

<template>
  <a :href="link">Login google</a>
</template>
