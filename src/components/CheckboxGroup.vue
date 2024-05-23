<template>
  <div class="checkbox-group">
    <input
      type="checkbox"
      :id="id"
      :name="name"
      :checked="modelValue"
      @change="updateValue($event.target.checked)"
      :required="required"
    />
    <label :for="id">{{ label }}</label>
  </div>
</template>

<script>
export default {
  props: {
    id: String,
    name: String,
    label: String,
    modelValue: Boolean,
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
.checkbox-group {
  display: flex;
  align-items: center;
  gap: 5px;
  text-align: left;
  font-weight: bold;
  cursor: pointer;
  margin-bottom: 20px;
}

.checkbox-group label {
  display: flex;
  align-items: center;
  gap: 5px;
  text-align: left;
  font-weight: bold;
  cursor: pointer;
}
</style>
