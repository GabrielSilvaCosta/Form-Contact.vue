<template>
    <div class="form-row">
      <slot></slot>
    </div>
  </template>
  
  <style scoped>
  .form-row {
    display: flex;
    flex-direction: column;
    gap: 20px;
    width: 100%;
    position: relative;
    margin-bottom: 20px;

  }
  </style>
  