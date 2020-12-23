<template>
<BaseFormInput class="email-input" input-id="birthday" label-display="Birthday" is-required="true">
  <input
      type="date"
      id="birthday"
      placeholder="1/1/1970"
      required=""
      :value="birthday"
      @input="$emit('update:birthday', $event.target.value)" >
</BaseFormInput>
</template>

<script>
import BaseFormInput from '@/components/BaseFormInput.vue';

export default {
  name: 'InputBirthday',
  components: {
    BaseFormInput,
  },
  props: {
    birthday: String,
  },
};
</script>

<style lang="scss">
</style>
