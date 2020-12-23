<template>
<BaseFormInput
    class="full-name"
    input-id="first-name"
    label-display="First Name"
    is-required="true">
  <input
      type="text"
      id="first-name"
      placeholder="First Name"
      required=""
      :value="firstName"
      @input="updateFirstName($event)" />
</BaseFormInput>
<BaseFormInput
    class="full-name"
    input-id="last-name"
    label-display="Last Name"
    is-required="true">
  <input
      type="text"
      id="last-name"
      placeholder="Last Name"
      required=""
      :value="lastName"
      @input="updateLastName($event)" />
</BaseFormInput>
</template>

<script>
import BaseFormInput from '@/components/BaseFormInput.vue';

export default {
  name: 'InputFullName',
  components: {
    BaseFormInput,
  },
  props: {
    firstName: String,
    lastName: String,
  },
  methods: {
    updateFirstName($e) {
      this.$emit('update:firstName', $e.target.value);
    },
    updateLastName($e) {
      this.$emit('update:lastName', $e.target.value);
    },
  },
};
</script>

<style lang="scss">
</style>
