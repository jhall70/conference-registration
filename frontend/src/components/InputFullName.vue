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
      @input="$emit('update:firstName', $event.target.value)" />
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
      @input="$emit('update:lastName', $event.target.value)" />
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
};
</script>

<style lang="scss">
</style>
