<template>
  <div>
    <div class="cursor-dot-outline"></div>
    <div class="cursor-dot"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      x: 0,
      y: 0
    }
  },
  computed: {
    style() {
      const { x, y } = this
      return {
        top: `${y}px`,
        left: `${x}px`
      }
    }
  },
  mounted() {
    const cursor = {
      delay: 8,
      _x: 0,
      _y: 0,
      endX: window.innerWidth / 2,
      endY: window.innerHeight / 2,
      cursorVisible: true,
      cursorEnlarged: false,
      $dot: document.querySelector('.cursor-dot'),
      $outline: document.querySelector('.cursor-dot-outline'),

      init() {
        // Set up element sizes
        this.dotSize = this.$dot.offsetWidth
        this.outlineSize = this.$outline.offsetWidth

        this.setupEventListeners()
        this.animateDotOutline()
      },

      //     updateCursor: function(e) {
      //         var self = this;

      //         console.log(e)

      //         // Show the cursor
      //         self.cursorVisible = true;
      //         self.toggleCursorVisibility();

      //         // Position the dot
      //         self.endX = e.pageX;
      //         self.endY = e.pageY;
      //         self.$dot.style.top = self.endY + 'px';
      //         self.$dot.style.left = self.endX + 'px';
      //     },

      setupEventListeners() {
        const self = this

        // Anchor hovering
        document.querySelectorAll('a').forEach(function(el) {
          el.addEventListener('mouseover', function() {
            self.cursorEnlarged = true
            self.toggleCursorSize()
          })
          el.addEventListener('mouseout', function() {
            self.cursorEnlarged = false
            self.toggleCursorSize()
          })
        })

        // Click events
        document.addEventListener('mousedown', function() {
          self.cursorEnlarged = true
          self.toggleCursorSize()
        })
        document.addEventListener('mouseup', function() {
          self.cursorEnlarged = false
          self.toggleCursorSize()
        })

        document.addEventListener('mousemove', function(e) {
          // Show the cursor
          self.cursorVisible = true
          self.toggleCursorVisibility()

          // Position the dot
          self.endX = e.pageX
          self.endY = e.pageY
          self.$dot.style.top = self.endY + 'px'
          self.$dot.style.left = self.endX + 'px'
        })

        // Hide/show cursor
        document.addEventListener('mouseenter', function(e) {
          self.cursorVisible = true
          self.toggleCursorVisibility()
          self.$dot.style.opacity = 1
          self.$outline.style.opacity = 1
        })

        document.addEventListener('mouseleave', function(e) {
          self.cursorVisible = true
          self.toggleCursorVisibility()
          self.$dot.style.opacity = 0
          self.$outline.style.opacity = 0
        })
      },

      animateDotOutline() {
        const self = this

        self._x += (self.endX - self._x) / self.delay
        self._y += (self.endY - self._y) / self.delay
        self.$outline.style.top = self._y + 'px'
        self.$outline.style.left = self._x + 'px'

        requestAnimationFrame(this.animateDotOutline.bind(self))
      },

      toggleCursorSize() {
        const self = this

        if (self.cursorEnlarged) {
          self.$dot.style.transform = 'translate(-50%, -50%) scale(0.75)'
          self.$outline.style.transform = 'translate(-50%, -50%) scale(1.5)'
        } else {
          self.$dot.style.transform = 'translate(-50%, -50%) scale(1)'
          self.$outline.style.transform = 'translate(-50%, -50%) scale(1)'
        }
      },

      toggleCursorVisibility() {
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
    if (!isMobile) cursor.init()
  }
}
</script>
<style lang="scss" scoped>
$primary: white;
$primary-light: white;
.cursor-dot,
.cursor-dot-outline {
  pointer-events: none;
  position: absolute;
  top: 50%;
  left: 50%;
  border-radius: 50%;
  opacity: 0;
  transform: translate(-50%, -50%);
  transition: opacity 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.cursor-dot {
  $size: 20px;
  width: $size;
  height: $size;
  border: 1px solid $primary;
}

.cursor-dot-outline {
  $size: 40px;
  width: $size;
  height: $size;
  background-color: rgba($primary-light, 0.3);
}
</style>
