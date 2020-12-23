<template>
  <div id="the-app">
    <h1>Conference Registration</h1>
    <p class="message"></p>
    <FormRegistration />
  </div>
</template>

<script>
import FormRegistration from '@/components/FormRegistration.vue';

export default {
  name: 'App',
  components: {
    FormRegistration,
  },
};
</script>

<style lang="scss">
</style>
