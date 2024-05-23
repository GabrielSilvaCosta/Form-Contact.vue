<template>
  <div class="form-group">
    <label :for="fore">{{ label }}</label>
    <slot></slot>
    <span class="error" v-if="errors">{{ errors }}</span>
  </div>
</template>

<script>
export default {
  props: {
    fore: String,
    label: String,
    errors: String,
  },
};
</script>

<style scoped>
.form-group {
  margin-bottom: 20px;
  flex: 1;
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: 5px;
  width: 100%;
  position: relative;
}

label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
  color: #555;
  text-align: left;
  font-size: 22px;
  line-height: 1.2;
  letter-spacing: 0.5px;
}

.error {
  color: red;
  font-size: 14px;
  margin-top: 5px;
  text-align: left;
}
</style>
