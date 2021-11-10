<template>
  <button
    class="custom-button"
    :class="{ 'custom-button_disabled': disabled }"
    :type="type"
    :disabled="disabled"
    v-on="$listeners"
  >
    <slot />
  </button>
</template>

<script>
export default {
  name: "CustomButton",
  props: {
    type: {
      type: String,
      default: "button",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped>
.custom-button {
  display: inline-block;
  box-sizing: border-box;
  margin: 0;
  padding: 12px 24px;
  font-size: 16px;
  line-height: 20px;
  cursor: pointer;
  transition: 0.2s ease-in;
  text-align: center;
  text-transform: uppercase;
  color: #ffffff;
  border: none;
  border-radius: 6px;
  background-color: #1e88e5;;
  box-shadow: 0 4px 8px rgba(54, 123, 245, 0.24);
}

.custom-button_disabled {
  pointer-events: none;
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
