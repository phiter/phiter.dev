<template>
  <section id="links">
    <ul class="links">
      <li v-for="{ icon, link, title, color } in links" :key="link" class="link">
        <a
          rel="noopener"
          class="link"
          target="_blank"
          :title="title"
          :href="link"
          :data-color="color"
        >
          <img :alt="title" :src="icon">
        </a>
      </li>
    </ul>
  </section>
</template>
<script setup>
const links = [
  {
    title: 'Github',
    link: 'https://github.com/phiter',
    icon: 'assets/svg/github.svg',
    color: '#000000'
  },
  {
    title: 'LinkedIn',
    link: 'https://linkedin.com/in/phiter/',
    icon: 'assets/svg/linkedin.svg',
    color: '#0077b5'
  },
  {
    title: 'StackOverflow',
    link: 'https://stackoverflow.com/users/4802649/phiter',
    icon: 'assets/svg/stackoverflow.svg',
    color: '#f48024'
  },
  {
    title: 'PluralSight',
    link: 'https://app.pluralsight.com/profile/phiter-martins',
    icon: 'assets/svg/pluralsight.svg',
    color: '#e91779'
  }
]
</script>
<style lang="scss">
.links {
  list-style: none;
  padding: 0;
  display: flex;
  justify-content: space-between;
  margin-top: 40px;
}

a.link {
  height: 30px;
  width: 30px;
  display: inline-block;
  animation-fill-mode: forwards;
  transform-origin: center;

  &:hover {
    animation: shake 0.3s ease;
  }

  margin: 0 20px;
}

@keyframes shake {
  0%,
  50%,
  100% {
    transform: rotate(0);
  }

  25% {
    transform: rotate(8deg);
  }

  75% {
    transform: rotate(-8deg);
  }
}
</style>
