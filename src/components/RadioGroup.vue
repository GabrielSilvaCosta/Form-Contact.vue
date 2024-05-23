<template>
  <div class="radio-group">
    <label v-for="option in options" :key="option.value" :for="option.value">
      <input
        type="radio"
        :id="option.value"
        :name="name"
        :value="option.value"
        :checked="option.value === modelValue"
        @change="updateValue(option.value)"
        :required="required"
      />
      {{ option.label }}
    </label>
  </div>
</template>

<script>
export default {
  props: {
    options: Array,
    name: String,
    modelValue: String,
    required: Boolean,
  },
  methods: {
    updateValue(value) {
      this.$emit("update:modelValue", value);
    },
  },
};
</script>

<style scoped>
.radio-group {
  display: flex;
  gap: 20px;
  flex-direction: column;
}

.radio-group label {
  display: flex;
  align-items: center;
  gap: 5px;
  text-align: left;
  font-weight: bold;
}
</style>
