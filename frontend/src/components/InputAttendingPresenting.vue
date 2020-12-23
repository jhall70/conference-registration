<template>
  <p>Are you attending, presenting, or both?</p>
  <BaseFormInput
    input-id="cause-error"
    label-display="Error option"
    is-required="true">
  <input
      type="radio"
      id="cause-error"
      value="cause-error"
      name="attendee-type"
      @change="$emit('update:attendeeType', $event.target.value)" />
  </BaseFormInput>
  <BaseFormInput v-for="type in attendeeTypes" :key="type.id"
                 :input-id="type.id"
                 :label-display="type.label"
                 is-required="true">
    <input
        type="radio"
        :id="type.id"
        :value="type.id"
        name="attendee-type"
        @change="$emit('update:attendeeType', $event.target.value)" />
  </BaseFormInput>
</template>

<script>
import BaseFormInput from '@/components/BaseFormInput.vue';

export default {
  name: 'InputAttendingPresenting',
  components: {
    BaseFormInput,
  },
  props: {
    attendeeType: String,
    attendeeTypes: Array,
  },
};
</script>

<style lang="scss">
</style>
