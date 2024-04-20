<template>
  <div>
    <input type="text" v-model.trim="phoneNumber" @blur="validatePhoneNumber">
    <p class="error" v-if="showError">The phone number must be exactly 11 digits long and start with '7'.</p>
    <button class="form__btn" @click="submit" :disabled="!isValid">Submit</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      phoneNumber: '',
      showError: false
    }
  },
  computed: {
    isValid() {
      return this.phoneNumber.length === 11 && /^7\d{10}$/.test(this.phoneNumber);
    }
  },
  methods: {
    validatePhoneNumber() {
      this.showError = !this.isValid;
    },
    submit() {
      // Handle form submission here
    }
  }
}
</script>

<style scoped>
.error {
  color: red;
  font-size: 0.8rem;
  margin-top: 5px;
}

.form__btn {
  background-color: blue;
  border: none;
  color: white;
  padding: 10px 20px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.form__btn:hover {
  background-color: darkblue;
}

.form__btn:focus {
  outline: none;
}

.form__btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>