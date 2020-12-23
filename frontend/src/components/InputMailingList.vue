<template>
<BaseFormInput
    class="mailing-list"
    input-id="mailing-list"
    label-display="I would like to join the mailing list"
    is-required="false">
  <input
      type="checkbox"
      id="mailing-list"
      :checked="mailingList === 'yes'"
      :value="mailingList"
      @change="$emit('update:mailingList', ($event.target.value === 'yes' ? 'no' : 'yes'))" />
</BaseFormInput>
</template>

<script>
import BaseFormInput from '@/components/BaseFormInput.vue';

export default {
  name: 'InputMailingList',
  components: {
    BaseFormInput,
  },
  props: {
    mailingList: String,
  },
};
</script>

<style lang="scss">
</style>
