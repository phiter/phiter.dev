<template>
  <div :style="{ color: currentLinkColor }">
    <div class="cursor-dot-outline" />
    <div class="cursor-dot" />
  </div>
</template>
<script>
export default {
  data () {
    return {
      currentLinkColor: null
    }
  },
  mounted () {
    const $vm = this
    const cursor = {
      delay: 8,
      _x: 0,
      _y: 0,
      endX: window.innerWidth / 2,
      endY: window.innerHeight / 2,
      cursorVisible: true,
      cursorEnlarged: false,
      isHoveringLink: false,
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
            this.cursorEnlarged = true
            this.isHoveringLink = true
            $vm.currentLinkColor = el.dataset.color
            this.toggleCursorSize()
          })
          el.addEventListener('mouseout', () => {
            this.cursorEnlarged = false
            this.isHoveringLink = false
            this.toggleCursorSize()
          })
        })

        // Click events
        document.addEventListener('mousedown', () => {
          this.cursorEnlarged = true
          this.toggleCursorSize()
        })
        document.addEventListener('mouseup', () => {
          this.cursorEnlarged = false
          this.toggleCursorSize()
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

      toggleCursorSize () {
        const self = this
        if (self.isHoveringLink) {
          self.$dot.classList.add('hovering-link')
          self.$outline.classList.add('hovering-link')
        } else {
          self.$dot.classList.remove('hovering-link')
          self.$outline.classList.remove('hovering-link')
        }
        if (self.cursorEnlarged) {
          self.$dot.style.transform = 'translate(-50%, -50%) scale(0.75)'
          self.$outline.style.transform = 'translate(-50%, -50%) scale(1.5)'
        } else {
          self.$dot.style.transform = 'translate(-50%, -50%) scale(1)'
          self.$outline.style.transform = 'translate(-50%, -50%) scale(1)'
        }
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
    const isMobile = /iPhone|iPad|iPod|Android/i.test(
      window.navigator.userAgent
    )
    if (!isMobile) { cursor.init() }
  }
}
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
  transform: translate(-50%, -50%);
  transition:
    opacity 0.3s ease-in-out,
    transform 0.3s ease-in-out,
    background-color 0.3s ease-in-out,
    border-color 0.3s ease-in-out;
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

  &.hovering-link {
    background-color: currentColor;
  }
}
</style>
