
<template>
  <div class="form">
    <form-builder :form="form" @onSubmit="handleFormSubmit" ref="fbuilder" />
    <button @click="this.$refs.fbuilder.submit()">Submit</button>
  </div>
</template>

<script>


import FormBuilder from '../components/FormBuilder/FormBuilder.vue';
import { required, email, minValue } from '@vuelidate/validators';

export default {
  data() {
    return {
      form: {
        username: { type: 'text', label: 'username', validators: { required } },
        email: { type: 'email', label: 'email', validators: { required, email } },
        age: { type: 'number', label: 'age', validators: { required, minValue: minValue(18) } }
      }
    };
  },
  methods: {
    handleFormSubmit({ isValid, form }) {
      if (isValid) {
        console.log('SUCCESS', form);
      }
      return;
    }
  },
  components: { FormBuilder }
}
</script>

<style scoped>
.form {
  max-width: 350px;
  display: flex;
  margin: auto;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.form input {
  width: 100%;
  margin-bottom: .5rem;
}

.form button {
  margin-top: 20px;
  cursor: pointer;
  border-radius: 5px;
  padding: 6px 30px;
  font-size: 13px;
  font-weight: 600;
  background: #fff;
  border: none;
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 10%), 0 1px 2px 0 rgb(0 0 0 / 6%);
  transition: all .3s;
}

.form button:hover {
  outline: none;
  border-color: #9ecaed;
  box-shadow: 0 0 10px #9ecaed;
  background-color: rgb(249, 250, 251);
  transition: all .3s;
}

.form button:focus {
  box-shadow: 0 0 3px #9ecaed;
  transition: all .3s;
}
</style>
