<template>
  <div class="container">
    <ul class="list">
      <li class="item" v-for="i in 100" :key="i">{{ i }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "lazyLoad",
  data() {
    return {};
  },
  methods: {
    initInterSectionObserver() {
      new IntersectionObserver(entries => {
        entries.map(item => {
          console.log(item);
        });
      });
    }
  },
  mounted() {}
};
</script>

<style scoped>
.container {
}
</style>
