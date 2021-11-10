<template>
  <label class="radio-input">
    <input
      type="radio"
      :name="name"
      :value="value"
      :checked="isChecked"
      class="radio-input__input"
      @change="$emit('change', $event)"
    />
    <span class="radio-input__label">{{ label }}</span>
  </label>
</template>

<script>
export default {
  name: "CustomRadioButton",
  props: {
    name: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    isChecked: {
      type: Boolean,
    },
  },
};
</script>

<style scoped>
.radio-input {
  cursor: pointer;
}

.radio-input__label {
  position: relative;
  display: inline-flex;
  align-items: center;
  font-size: 16px;
  line-height: 19px;
  color: rgba(34, 60, 80, 0.6);
}

.radio-input__label:before {
  display: block;
  box-sizing: border-box;
  width: 20px;
  height: 20px;
  margin-right: 16px;
  content: "";
  transition: 0.2s ease-in;
  border: 1px solid #b3abbc;
  border-radius: 50%;
  background-color: #ffffff;
}

.radio-input__label:hover input:not(:checked):not(:disabled) + span:before {
  border-color: #685879;
}

.radio-input__input {
  display: none;
}

.radio-input__input:checked + span:before {
  border: 6px solid #1e88e5;
}

.radio-input__input:disabled + span:before {
  border-color: #b3abbc;
  background-color: #eaeaea;
}

.radio-input__input:disabled:checked + span :before {
  border: 6px solid #b3abbc;
}
</style>
