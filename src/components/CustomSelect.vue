<template>
  <div class="custom-select">
    <label v-if="label" class="custom-select__label">
      {{ label }}
    </label>
    <input
      class="custom-select__input"
      :name="name"
      :value="searchFilter"
      @focus="showOptions()"
      @blur="exit()"
      @keyup="keyMonitor"
      @input="debouncedInput"
      :placeholder="placeholder"
    />
    <div class="custom-select__content" v-show="optionsShown">
      <div
        v-for="(option, index) in filteredOptions"
        :key="index"
        class="custom-select__item"
        @mousedown="selectOption(option)"
      >
        {{ option.name || option.id || "-" }}
      </div>
    </div>
  </div>
</template>

<script>
import { debounce } from "../utils/debounce";

export default {
  name: "custom-select",
  template: "custom-select",
  props: {
    name: {
      type: String,
      required: false,
      default: "custom-select",
    },
    label: {
      type: String,
      required: false,
      default: "",
    },
    options: {
      type: Array,
      required: true,
      default: () => [],
    },
    placeholder: {
      type: String,
      required: false,
    },
    maxItem: {
      type: Number,
      required: false,
      default: 6,
    },
  },
  data() {
    return {
      selected: {},
      optionsShown: false,
      searchFilter: "",
    };
  },
  computed: {
    filteredOptions() {
      const filtered = [];
      const regOption = new RegExp(this.searchFilter, "ig");
      for (const option of this.options) {
        if (this.searchFilter.length < 1 || option.name.match(regOption)) {
          if (filtered.length < this.maxItem) filtered.push(option);
        }
      }
      return filtered;
    },
  },
  methods: {
    debouncedInput: debounce(function (event) {
      this.searchFilter = event.target.value;
    }, 500),
    selectOption(option) {
      this.selected = option;
      this.optionsShown = false;
      this.searchFilter = option.name;
      this.$emit("selected", this.selected);
    },
    showOptions() {
      this.searchFilter = "";
      this.optionsShown = true;
    },
    exit() {
      this.optionsShown = false;
    },
    keyMonitor(event) {
      if (event.key === "Enter" && this.filteredOptions[0])
        this.selectOption(this.filteredOptions[0]);
    },
  },
};
</script>

<style scoped>
.custom-select {
  position: relative;
}

.custom-select__label {
  display: block;
  margin: 0 0 8px;
  color: rgba(34, 60, 80, 0.6);
}

.custom-select__input {
  display: block;
  box-sizing: border-box;
  width: 100%;
  margin: 0;
  padding: 12px 16px;
  color: rgba(33, 33, 33, 0.87);
  border: 1px solid #f1f3f4;
  border-radius: 6px;
}

.custom-select__input::placeholder {
  color: #b3abbc;
}

.custom-select__input:focus {
  border-color: #1e88e5;
}

.custom-select__content {
  position: absolute;
  background-color: #ffffff;
  left: 0;
  right: 0;
  z-index: 1;
  max-height: 300px;
  border: 1px solid #f1f3f4;
  box-shadow: 0 -8px 34px 0 rgba(0, 0, 0, 0.05);
  overflow: auto;
}

.custom-select__item {
  color: rgba(33, 33, 33, 0.87);
  font-size: 14px;
  line-height: 18px;
  padding: 8px 16px;
  text-decoration: none;
  display: block;
  cursor: pointer;
}

.custom-select__item:not(:last-child) {
  border-bottom: 1px solid #f1f3f4;
}

.custom-select__item:hover {
  background-color: #e7ecf5;
}

.custom-select:hover .custom-select__content {
  display: block;
}
</style>
