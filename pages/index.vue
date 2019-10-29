<template>
  <div class="container">
    <section id="main">
      <h1>
        Phiter Fernandes
      </h1>
      <h2>Web Developer</h2>
      <social-links :links="links" />
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
import SocialLinks from '~/components/SocialLinks.vue'
import CustomCursor from '~/components/Cursor.vue'

export default {
  components: {
    SocialLinks,
    CustomCursor
  },
  head() {
    return {
      title: 'Phiter Fernandes - Web Developer',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: "Hi, I'm Phiter, a Web Developer. This is my website :)"
        }
      ]
    }
  },
  data() {
    return {
      links: [
        {
          title: 'Github',
          link: 'https://github.com/phiter',
          icon: 'GithubIcon'
        },
        {
          title: 'LinkedIn',
          link: 'https://linkedin.com/in/phiter/',
          icon: 'LinkedinIcon'
        },
        {
          title: 'Twitter',
          link: 'https://twitter.com/phiterf',
          icon: 'TwitterIcon'
        }
      ]
    }
  }
}
</script>

<style lang="scss">
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
  color: #ffffff;
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
