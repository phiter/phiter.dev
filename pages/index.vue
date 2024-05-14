<template>
  <div class="container">
    <section id="main">
      <h1>Phiter Fernandes</h1>
      <h2>Web Developer</h2>
      <SocialLinks />

      <BlogLink />
    </section>
    <ClientOnly>
      <custom-cursor v-if="!isMobile" />
    </ClientOnly>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
const isMobile = ref(false);

onMounted(() => {
  isMobile.value = /iPhone|iPad|iPod|Android/i.test(window.navigator.userAgent);
});
useHead({
    title: 'Phiter Fernandes - Web Developer',
    meta: [
        {
        hid: 'description',
        name: 'description',
        content: "Hi, I'm Phiter, a Web Developer. This is my website :)"
        },
    ],
    link: [
        {
          rel: 'stylesheet',
          href: 'https://fonts.googleapis.com/css?family=Raleway&display=swap',
          defer: true
        }
    ]
});

</script>

<style>
body {
  font-family: 'Raleway', sans-serif;
  background-color: #1a1b2b;
  color: white;
}

#main {
  z-index: 10;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  opacity: 0.9;
}

h1 {
  font-size: 50px;
  margin-bottom: 10px;
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
