<template>
  <div class="text-field">
    <label v-if="label" class="text-field__label">
      {{ label }}
    </label>
    <input
      ref="input"
      :value="value"
      :type="type"
      :name="name"
      :placeholder="placeholder"
      class="text-field__input"
      :class="{ 'text-field__input--error': showError }"
      @input="$emit('input', $event)"
    />
    <span v-if="showError" class="text-field__text">
      {{ errorText }}
    </span>
  </div>
</template>

<script>
export default {
  name: "CustomInput",
  model: {
    prop: "value",
    event: "input",
  },
  props: {
    value: {
      type: [String, Number],
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: false,
    },
    type: {
      type: String,
      default: "text",
    },
    placeholder: {
      type: String,
      default: "",
    },
    errorText: {
      type: String,
      default: "",
    },
    required: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    showError() {
      return !!this.errorText;
    },
  },
};
</script>

<style scoped>
.text-field {
  position: relative;
}

.text-field__label {
  display: block;
  margin: 0 0 8px;
  color: rgba(34, 60, 80, 0.6);
}

.text-field__input {
  display: block;
  box-sizing: border-box;
  width: 100%;
  margin: 0;
  padding: 12px 16px;
  font-family: inherit;
  color: rgba(33, 33, 33, 0.87);
  border: 1px solid #f1f3f4;
  border-radius: 6px;
}

.text-field__input::placeholder {
  color: #b3abbc;
}

.text-field__input--error {
  border-color: #e53935;
}

.text-field__input:focus {
  border-color: #1e88e5;
}

.text-field__text {
  position: absolute;
  bottom: -12px;
  left: 0;
  color: #e53935;
  font-size: 10px;
  line-height: 12px;
}
</style>
