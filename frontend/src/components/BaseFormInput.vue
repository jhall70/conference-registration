<template>
  <div class="labeled-input"  :isrequired="isRequired">
    <label :for="inputId">{{ labelDisplay }}</label>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'BaseFormInput',
  props: {
    inputId: String,
    labelDisplay: String,
    isRequired: Boolean,
  },
};
</script>

<style lang="scss">
</style>
