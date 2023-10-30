<template>
  <header>

    <div class="wrapper">
      <div>
        <list-component></list-component>
      </div>
    </div>
  </header>
  
  <!-- <RouterView /> -->
</template>

<style scoped></style>

<script>
import ListComponent from './views/ListComponent.vue';
import zoomSdk from '@zoom/appssdk';
export default {
  components: {
    ListComponent,
  },
};
</script>
