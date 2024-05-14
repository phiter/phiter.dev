<template>
  <div
    :style="{ color: currentLinkColor }"
    class="cursor-wrapper"
    :class="{
      'hovering-link' : isHoveringLink,
      'enlarged': cursorEnlarged,
      'super-enlarged': cursorSuperEnlarged
    }"
  >
    <div
      class="cursor-dot-outline"
    />
    <div class="cursor-dot" />
  </div>
</template>
<script setup>
import { ref } from 'vue';

const currentLinkColor = ref(null);
const isHoveringLink = ref(false);
const cursorEnlarged = ref(false);
const cursorSuperEnlarged = ref(false);

onMounted(() => {
  const cursor = {
    delay: 8,
    _x: 0,
    _y: 0,
    endX: window.innerWidth / 2,
    endY: window.innerHeight / 2,
    cursorVisible: true,
    cursorEnlarged: false,
    isHoveringLink: false,
    enlargedSize: 1.5,
    $dot: document.querySelector('.cursor-dot'),
    $outline: document.querySelector('.cursor-dot-outline'),

    init () {
      // Set up element sizes
      this.dotSize = this.$dot.offsetWidth
      this.outlineSize = this.$outline.offsetWidth

      this.setupEventListeners()
      this.animateDotOutline()
    },
    setupEventListeners () {
      document.querySelectorAll('a').forEach((el) => {
        el.addEventListener('mouseover', () => {
          cursorEnlarged.value = true
          cursorSuperEnlarged.value = !!el.dataset.superenlarge
          isHoveringLink.value = true
          currentLinkColor.value = el.dataset.color
        })
        el.addEventListener('mouseout', () => {
          cursorEnlarged.value = false
          cursorSuperEnlarged.value = false
          isHoveringLink.value = false
        })
      })

      // Click events
      document.addEventListener('mousedown', () => {
        cursorEnlarged.value = true
      })
      document.addEventListener('mouseup', () => {
        cursorEnlarged.value = false
      })

      document.addEventListener('mousemove', (e) => {
        // Show the cursor
        this.cursorVisible = true
        this.toggleCursorVisibility()

        // Position the dot
        this.endX = e.pageX
        this.endY = e.pageY
        this.$dot.style.top = this.endY + 'px'
        this.$dot.style.left = this.endX + 'px'
      })

      // Hide/show cursor
      document.addEventListener('mouseenter', (e) => {
        this.cursorVisible = true
        this.toggleCursorVisibility()
        this.$dot.style.opacity = 1
        this.$outline.style.opacity = 1
      })

      document.addEventListener('mouseleave', (e) => {
        this.cursorVisible = true
        this.toggleCursorVisibility()
        this.$dot.style.opacity = 0
        this.$outline.style.opacity = 0
      })
    },

    animateDotOutline () {
      const self = this

      self._x += (self.endX - self._x) / self.delay
      self._y += (self.endY - self._y) / self.delay
      self.$outline.style.top = self._y + 'px'
      self.$outline.style.left = self._x + 'px'

      requestAnimationFrame(this.animateDotOutline.bind(self))
    },

    toggleCursorVisibility () {
      const self = this

      if (self.cursorVisible) {
        self.$dot.style.opacity = 1
        self.$outline.style.opacity = 1
      } else {
        self.$dot.style.opacity = 0
        self.$outline.style.opacity = 0
      }
    }
  }

  cursor.init()
})
</script>
<style lang="scss">
$primary: white;
$secondary: #2d38ce;

html,
body {
  &,
  * {
    cursor: none;
  }
}

.cursor-dot,
.cursor-dot-outline {
  pointer-events: none;
  position: fixed;
  top: 50%;
  left: 50%;
  border-radius: 50%;
  opacity: 0;
  transform: translate(-50%, -50%) scale(1);
  transition:
    opacity 0.25s ease-in-out,
    transform 0.25s ease-in-out,
    background-color 0.25s ease-in-out,
    border-color 0.25s ease-in-out;
}

.cursor-dot {
  $size: 20px;

  width: $size;
  height: $size;
  border: 1px solid $primary;
  z-index: 1000;
}

.cursor-dot-outline {
  $size: 40px;

  width: $size;
  height: $size;
  background-color: rgba($primary, 0.3);
}

.cursor-wrapper {
  &.hovering-link {
    .cursor-dot {
      background: currentColor;
    }

    .cursor-dot-outline {
      background-color: currentColor;
    }
  }

  &.enlarged {
    .cursor-dot {
      transform: translate(-50%, -50%) scale(0.75);
    }

    .cursor-dot-outline {
      transform: translate(-50%, -50%) scale(1.5);
    }
  }

  &.super-enlarged {
    .cursor-dot-outline {
      transform: translate(-50%, -50%) scale(10);
    }
  }
}
</style>
