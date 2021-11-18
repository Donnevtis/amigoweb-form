<script lang="ts">
export default {
  props: { modelValue: Boolean },
  methods: {
    emitCheck(e) {
      this.$emit("update:modelValue", e.target.checked as boolean);
    },
  },
};
</script>
<template>
  <div class="FormCheckbox">
    <input
      type="checkbox"
      class="FormCheckbox__input"
      name="FormCheckbox"
      id="FormCheckbox"
      @change="emitCheck"
    />

    <label for="FormCheckbox"><slot></slot></label>
  </div>
</template>
<style lang="scss">
.FormCheckbox {
  padding: 8px;
}
.FormCheckbox__input {
  position: absolute;
  z-index: -1;
  opacity: 0;
  width: 1px;
  height: 1px;
  & + label {
    display: inline-flex;
    align-items: center;
    user-select: none;
    &::before {
      content: "";
      display: inline-block;
      width: 28px;
      height: 28px;
      flex-shrink: 0;
      flex-grow: 0;
      border: 1px solid #dbe2ea;
      border-radius: 4px;
      margin-right: 8px;
      background-repeat: no-repeat;
      background-position: center center;
      box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    }
    &:hover::before {
      border-width: 2px;
    }
  }
  &:checked + label::before {
    background-color: #fff;
    border: 2px solid #0880ae;
    background-image: url("../../assets/svg/Mask.svg");
  }
}
</style>
