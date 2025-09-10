<!-- filepath: ShootingStarsBackground.vue -->
<template>
  <div class="shooting-stars">
    <div v-for="n in 8" :key="n" class="shooting-star"></div>
  </div>
</template>

<script>
export default {
  name: 'ShootingStarsBackground',
  mounted() {
    this.interval = setInterval(() => {
      if (Math.random() > 0.3) {
        this.createShootingStar();
      }
    }, Math.random() * 5000 + 3000);
  },
  beforeUnmount() {
    clearInterval(this.interval);
  },
  methods: {
    createShootingStar() {
      const star = document.createElement('div');
      star.className = 'shooting-star';
      star.style.top = Math.random() * 60 + '%';
      star.style.animationDelay = '0s';
      star.style.animationDuration = (Math.random() * 1.5 + 2) + 's';
      this.$el.appendChild(star);
      setTimeout(() => {
        star.remove();
      }, 4000);
    }
  }
}
</script>

<style scoped>
*,
*::after,
*::before {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

:root {
  --dark-color: #000;
  --fl-speed: 0.8s;
  --speed-leaf: 2s;
}

.shooting-stars {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  pointer-events: none;
  z-index: 1;
}

.shooting-star {
  position: absolute;
  width: 4px;
  height: 4px;
  background: #fff;
  border-radius: 50%;
  box-shadow: 0 0 6px 2px rgba(255, 255, 255, 0.8);
  opacity: 0;
  animation: shootingStar 3s linear infinite;
}

.shooting-star::before {
  content: '';
  position: absolute;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 1) 100%);
  animation: shootingStarTail 3s linear infinite;
}

.shooting-star:nth-child(1) {
  top: 5%;
  left: -10%;
  animation-delay: 0s;
  animation-duration: 2.5s;
}

.shooting-star:nth-child(2) {
  top: 15%;
  left: -10%;
  animation-delay: 2s;
  animation-duration: 3s;
}

.shooting-star:nth-child(3) {
  top: 25%;
  left: -10%;
  animation-delay: 4s;
  animation-duration: 2.8s;
}

.shooting-star:nth-child(4) {
  top: 0%;
  left: -10%;
  animation-delay: 6s;
  animation-duration: 3.2s;
}

.shooting-star:nth-child(5) {
  top: 35%;
  left: -10%;
  animation-delay: 8s;
  animation-duration: 2.7s;
}

.shooting-star:nth-child(6) {
  top: 8%;
  left: -10%;
  animation-delay: 10s;
  animation-duration: 3.1s;
}

.shooting-star:nth-child(7) {
  top: 45%;
  left: -10%;
  animation-delay: 12s;
  animation-duration: 2.9s;
}

.shooting-star:nth-child(8) {
  top: 3%;
  left: -10%;
  animation-delay: 14s;
  animation-duration: 3.3s;
}

@keyframes shootingStar {
  0% {
    opacity: 0;
    transform: translateX(0) translateY(0) rotate(45deg);
  }
  10% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: translateX(120vw) translateY(50vh) rotate(10deg);
  }
}

@keyframes shootingStarTail {
  0% {
    width: 0;
  }
  30% {
    width: 100px;
  }
  100% {
    width: 0;
  }
}
</style>