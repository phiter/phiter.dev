<template>
  <section id="links">
    <ul class="links">
      <li v-for="{ icon, link, title } in links" :key="link" class="link">
        <a target="_blank" :title="title" :href="link">
          <component :is="icon" />
        </a>
      </li>
    </ul>
  </section>
</template>
<script>
import GithubIcon from '~/components/GithubIcon'
import LinkedinIcon from '~/components/LinkedinIcon'
import TwitterIcon from '~/components/TwitterIcon'

export default {
  components: {
    GithubIcon,
    LinkedinIcon,
    TwitterIcon
  },
  props: {
    links: {
      type: Array,
      required: true
    }
  }
}
</script>
<style lang="scss">
.links {
  list-style: none;
  padding: 0;
  display: flex;
  justify-content: space-between;
  margin-top: 40px;
}
a {
  height: 30px;
  width: 30px;
  display: inline-block;
  margin: 0 20px;
}
</style>
