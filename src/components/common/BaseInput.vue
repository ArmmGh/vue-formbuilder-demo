<template>
  <div class="field">
    <label> {{ label }} </label>
    <input v-bind="$attrs" :placeholder="label" :type="type" class="field" :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)">
    <div class="errors" v-for="error of errors" :key="error.$uid">
      <p class="error">{{ error.$message }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    errors: {
      type: Object
    },
    type: {
      type: String,
      default: 'text'
    },
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    }
  }
}
</script>

<style scoped>
.field {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: flex-start;
  padding: 5px;
}

.field label {
  font-weight: 600;
  font-size: 12px;
  margin-bottom: 2px;
}

.field input::placeholder {
  color: #dadada;
}

.field input {
  border: 2px solid #dadada;
  border-radius: 7px;
  transition: all .3s;
}

.field input:focus {
  outline: none;
  border-color: #9ecaed;
  box-shadow: 0 0 10px #9ecaed;
  transition: all .3s;
}

.field .errors {}

.field .errors p {
  margin: 0;
  padding: 0;
  font-size: 12.5px;
  font-weight: 500;
  color: red;
}
</style>
