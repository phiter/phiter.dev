<template>
  <section id="links">
    <ul class="links">
      <li v-for="{ icon, link, title } in links" :key="link" class="link">
        <a
          rel="noopener"
          class="link"
          target="_blank"
          :title="title"
          :href="link"
        >
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
import StackOverflowIcon from '~/components/StackOverflowIcon'
import PluralSightIcon from '~/components/PluralSightIcon'

export default {
  components: {
    GithubIcon,
    LinkedinIcon,
    TwitterIcon,
    StackOverflowIcon,
    PluralSightIcon
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
    transform: rotate(5deg);
  }
  75% {
    transform: rotate(-5deg);
  }
}
</style>
