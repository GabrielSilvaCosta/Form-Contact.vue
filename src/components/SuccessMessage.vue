<template>
  <div class="success-message" aria-live="polite">
    {{ message }}
  </div>
</template>

<script>
export default {
  props: {
    message: String,
  },
};
</script>

<style scoped>
.success-message {
  margin-top: 20px;
  color: green;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
}
</style>
