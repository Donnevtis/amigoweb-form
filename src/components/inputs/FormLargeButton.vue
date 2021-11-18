<script setup lang="ts">
defineProps<{ value: string; type: string; disabled: boolean }>();
</script>
<template>
  <div class="FormButton-large">
    <input :type="type" :value="value" :disabled="disabled" />
  </div>
</template>
<style lang="scss">
.FormButton-large {
  position: relative;
  z-index: 1;
  padding: 8px;
  input {
    position: relative;
    z-index: 1;
    height: 56px;
    width: 100%;
    background: #0880ae;
    box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
      0px 4px 8px rgba(44, 39, 56, 0.08);
    border-radius: 6px;
    color: #ebf4f8;
    font-family: IBM Plex Sans;
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
  }
  input:not(:disabled):hover {
    border: 2px solid #2c2738db;
  }
  input:disabled {
    color: #2c2738;
    mix-blend-mode: normal;
    opacity: 0.5;
    color: #2c2738;
    background: #dbe2ea;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.08);
  }
}
</style>
