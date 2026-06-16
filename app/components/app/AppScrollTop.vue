<template>
  <Transition name="scroll-top">
    <button
      v-if="visible"
      class="scroll-top"
      @click="scrollToTop"
      aria-label="Наверх"
    >
      ↑
    </button>
  </Transition>
</template>

<script setup>
const visible = ref(false);

const handleScroll = () => {
  visible.value = window.scrollY > 400;
};

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  handleScroll();
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<style lang="less">
.scroll-top {
  position: fixed;
  right: 30px;
  bottom: 30px;
  z-index: 200;

  width: 50px;
  height: 50px;

  border: none;
  border-radius: 50%;

  background-color: transparent;
  color: @black;

  font-size: 24px;
  cursor: pointer;

  transition: transform 0.2s, opacity 0.2s;

  &:hover {
    transform: translateY(-3px);
  }

  @media @bw768 {
    right: 20px;
    bottom: 20px;
  }
}

.scroll-top-enter-active,
.scroll-top-leave-active {
  transition: opacity 0.3s, transform 0.3s;
}

.scroll-top-enter-from,
.scroll-top-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
</style>