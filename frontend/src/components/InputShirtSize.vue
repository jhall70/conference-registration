<template>
<BaseFormInput
    class="labeled-select"
    input-id="shirt-size"
    label-display="Shirt Size"
    is-required="true">
  <select id="shirt-size" required="" @change="$emit('update:shirtSize', $event.target.value)">
    <option disabled="" :selected="shirtSize === ''">Please select an option:</option>
    <option value="cause-error">This will throw an error</option>
    <option
        v-for="size in shirtSizes"
        :key="size.value"
        :value="size.value">{{ size.label }}</option>
  </select>
</BaseFormInput>
</template>

<script>
import BaseFormInput from '@/components/BaseFormInput.vue';

export default {
  name: 'InputShirtSize',
  components: {
    BaseFormInput,
  },
  props: {
    shirtSize: String,
    shirtSizes: Array,
  },
};
</script>

<style lang="scss">
</style>
