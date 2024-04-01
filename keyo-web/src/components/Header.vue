<template>
  <header ref="headerRef" class="header" :class="{ scrolledDown: isScrolledDown, scrolledUp: isScrolledUp }">
    <div id="header-content">
      <h4>Logo</h4>
      <h4>SideMenu</h4>
    </div>
  </header>
</template>

<script>
import { ref, computed, onMounted, onUnmounted } from 'vue';

export default {
  name: 'AppHeader',
  setup() {
    const headerRef = ref(null);
    const isScrolledDown = ref(false);
    const isScrolledUp = ref(false);

    const handleScroll = () => {
      const currScrollPos = window.pageYOffset;
      const dir = currScrollPos > prevScrollPos ? 'down' : 'up';
      prevScrollPos = currScrollPos;

      isScrolledDown.value = dir === 'down';
      isScrolledUp.value = dir === 'up';
    };

    let prevScrollPos = window.pageYOffset;

    onMounted(() => {
      window.addEventListener('scroll', handleScroll);
    });

    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll);
    });

    return {
      isScrolledDown,
      isScrolledUp,
    };
  },
};
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  min-height: 60px;
  padding: 1rem;
  box-sizing: border-box;
  z-index: 1000;
  background-color: white;
  border-bottom: 1px solid #ddd;
  transition: transform 0.3s ease-in-out;
}

.scrolledDown {
  transform: translateY(-100%);
}

.scrolledUp {
  transform: translateY(0);
}

#header-content {
  color: red;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 1rem;
}
</style>