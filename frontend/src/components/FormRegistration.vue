<template>
  <p v-if="successMessage" class="error">{{successMessage}}</p>

  <!-- prevent is like event.preventDefault() -->
  <form v-else @submit.prevent="createRegistration">
  <fieldset>
    <InputFullName v-model:first-name="firstName" v-model:last-name="lastName"/>
  </fieldset>
  <fieldset>
    <InputEmail v-model:email="email"/>
  </fieldset>
  <fieldset>
    <InputBirthday v-model:birthday="birthday"/>
    <InputShirtSize v-model:shirt-size="shirtSize" :shirt-sizes="shirtSizes"/>
  </fieldset>
  <fieldset class="radio-group">
    <InputAttendingPresenting v-model:attendee-type="attendeeType" :attendee-types="attendeeTypes"/>
  </fieldset>
  <fieldset class="checkbox-group">
    <InputMailingList v-model:mailing-list="mailingList" />
  </fieldset>
  <ButtonSubmit @submitEvent="checkRegistration"/>
  <div v-if="errors.length">
    <b>Please correct the following error(s):</b>
  <ul>
    <li v-for="error in errors" :key="error">{{ error }}</li>
  </ul>
  </div>
</form>
</template>

<script>
import InputFullName from '@/components/InputFullName.vue';
import InputEmail from '@/components/InputEmail.vue';
import InputBirthday from '@/components/InputBirthday.vue';
import InputShirtSize from '@/components/InputShirtSize.vue';
import InputAttendingPresenting from '@/components/InputAttendingPresenting.vue';
import InputMailingList from '@/components/InputMailingList.vue';
import ButtonSubmit from '@/components/ButtonSubmit.vue';

export default {
  name: 'FormRegistration',
  components: {
    InputFullName,
    InputEmail,
    InputBirthday,
    InputShirtSize,
    InputAttendingPresenting,
    InputMailingList,
    ButtonSubmit,
  },
  data() {
    return {
      firstName: '',
      lastName: '',
      email: '',
      birthday: '',
      shirtSize: '',
      attendeeType: '',
      mailingList: 'yes',
      successMessage: '',
      errors: [],
      emailReg: /^(([^<>()\]\\.,;:\s@"]+(\.[^<>()\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/,
      dateReg: /^\d{4}[/-]\d{2}[/-]\d{2}$/,

    };
  },
  computed: {
    shirtSizes() {
      return [{
        value: 's',
        label: 'Small',
      }, {
        value: 'm',
        label: 'Medium',
      }, {
        value: 'l',
        label: 'Large',
      }, {
        value: 'xl',
        label: 'XL',
      }, {
        value: 'xxl',
        label: 'XXL',
      }, {
        value: 'xxxl',
        label: 'XXXL',
      }, {
        value: 'xxxxl',
        label: 'XXXXL',
      }, {
        value: 'xxxxxl',
        label: 'XXXXXL',
      }];
    },
    attendeeTypes() {
      return [{
        id: 'attending',
        label: 'Attending',
      }, {
        id: 'presenting',
        label: 'Presenting',
      }, {
        id: 'both',
        label: 'Both',
      }];
    },
  },
  methods: {
    checkEmail() {
      if (this.email == null || this.email === '') {
        this.errors.push('Please Enter Email');
      } else if (!this.emailReg.test(this.email)) {
        this.errors.push('Please enter a valid email');
      }
    },
    checkBirthday() {
      if (this.birthday == null || this.birthday === '') {
        this.errors.push('Please Enter Birthday');
      } else if (!this.dateReg.test(this.birthday)) {
        this.errors.push('Please enter a valid date for birthday in the format MM-DD-YYYY');
      }
    },
    checkName() {
      if (!this.firstName) {
        this.errors.push('First name is required.');
      }
      if (!this.lastName) {
        this.errors.push('Last name is required.');
      }
    },
    checkShirtSize() {
      if (!this.shirtSizes.some((size) => size.value === this.shirtSize)) {
        this.errors.push('Please choose a shirt size from the list.');
      }
    },
    checkAttendeeType() {
      if (!this.attendeeTypes.some((type) => type.id === this.attendeeType)) {
        this.errors.push('Please choose a attendee type from the list.');
      }
    },
    checkMailingList() {
      this.mailingList = 'shit';
      const mailingListOptions = ['yes', 'no'];
      if (!mailingListOptions.some((option) => option === this.mailingList)) {
        this.errors.push("Please don't submit bullshit.");
      }
    },
    checkRegistration() {
      this.errors = [];
      this.checkName();
      this.checkBirthday();
      this.checkEmail();
      this.checkShirtSize();
      this.checkAttendeeType();
      this.checkMailingList();
      return this.errors.length === 0;
    },
    createRegistration() {
      if (this.checkRegistration()) {
        fetch('http://localhost:8091/registration', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            registration: {
              firstName: this.firstName,
              lastName: this.lastName,
              email: this.email,
              birthday: this.birthday,
              shirtSize: this.shirtSize,
              attendeeType: this.attendeeType,
              mailingList: this.mailingList,
            },
          }),
        })
          .then((response) => response.json())
          .then((response) => {
          // success message
            if (response.error) {
              this.errors.push(`It didn't work!: ${response.error}`);
            } else if (response.message) {
              this.successMessage = `${response.message}`;
            }
          })
          .catch(() => {
          // fail message
            this.errors.push("It didn't work!");
          });
      }
    },
  },
};
</script>

<style lang="scss">
</style>
