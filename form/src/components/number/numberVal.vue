<template>
  <input type="tel" v-model="boundValue" @blur="validatePhoneNumber" required />
</template>

<script>
export default {
  name: "inputPhone",
  props: {
    value: String,
  },
  computed: {
    boundValue: {
      get() {
        return this.value || '';
      },
      set(newValue) {
        this.$emit('input', newValue);
      },
    },
  },
  methods: {
    validatePhoneNumber() {
      if (!this.boundValue || !/^[7]\d{10}$/.test(this.boundValue)) {
        this.boundValue = '';
        this.$emit('input', '');
        this.$emit('update:modelValue', '');
      }
    },
  },
};
</script>

<style scoped>
input[type='tel'] {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}
</style>