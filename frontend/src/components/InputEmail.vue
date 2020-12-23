<template>
<BaseFormInput class="email-input" input-id="email" label-display="Email" is-required="true">
  <input
      type="email"
      id="email"
      placeholder="kyle@sikaeducation.com"
      required=""
      :value="email"
      @input="$emit('update:email', $event.target.value)" />
</BaseFormInput>
</template>

<script>
import BaseFormInput from '@/components/BaseFormInput.vue';

export default {
  name: 'InputEmail',
  components: {
    BaseFormInput,
  },
  props: {
    email: String,
  },
};
</script>

<style lang="scss">
</style>
