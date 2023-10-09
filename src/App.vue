<template>
  <main>
    <example-directivas />
  </main>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import ExampleDirectivas from './components/ExampleDirectivas.vue';

export default defineComponent({
  name: 'App',
  components: {
    ExampleDirectivas,
  }
});

</script>
<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  }
  main {
  display: flex;
  padding: auto;
  flex-direction: column;
  /* center the content */
  justify-content: center;
  }
</style>
