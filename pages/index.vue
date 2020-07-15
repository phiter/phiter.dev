<template>
  <div class="container">
    <section id="main">
      <h1>Phiter Fernandes</h1>
      <h2>Web Developer</h2>
      <social-links />
    </section>
    <vue-particles
      color="#332657"
      :particle-opacity="0.5"
      :lines-distance="200"
      :particles-number="15"
      :move-speed="4"
    />
    <custom-cursor />
  </div>
</template>

<script>
export default {
  head () {
    return {
      title: 'Phiter Fernandes - Web Developer',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: "Hi, I'm Phiter, a Web Developer. This is my website :)"
        }
      ],
      link: [
        {
          rel: 'stylesheet',
          href: 'https://fonts.googleapis.com/css?family=Raleway&display=swap',
          defer: true
        }
      ]
    }
  }
}
</script>

<style>
#particles-js {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}

body {
  font-family: 'Raleway', sans-serif;
  background-color: #1a1b2b;
  color: theme('colors.white');
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
