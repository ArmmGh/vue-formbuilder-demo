<template>
  <base-input v-for="(field, key, index) in form" v-model="dynamicModel[key]" :key="index" :label="field.label"
    :type="field.type" :errors="v$.dynamicModel[key] && v$.dynamicModel[key].$errors" />
</template>

<script>
import useVuelidate from '@vuelidate/core'
import BaseInput from '../common/BaseInput.vue'

export default {
  props: {
    form: {
      type: Object
    },
  },
  emits: {
    onSubmit: { type: Object }
  },
  data() {
    return {
      v$: useVuelidate(),
      dynamicModel: {},
      validators: {}
    }
  },
  beforeMount() {
    for (const [key, control] of Object.entries(this.form)) {
      this.dynamicModel[key] = control.default || '';
      this.validators[key] = control.validators;
    }
  },
  methods: {
    async submit() {
      const isValid = await this.v$.$validate();
      this.$emit('onSubmit', { isValid, form: this.dynamicModel })
    }
  },
  validations() {
    return {
      dynamicModel: { ...this.validators }
    };
  },
  components: {
    BaseInput
  }
}
</script>

<style>
</style>
