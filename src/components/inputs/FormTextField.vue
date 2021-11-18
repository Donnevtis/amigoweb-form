<script setup lang="ts">
import { ref, computed } from "vue";
const { field } = defineProps<{
  field: {
    value: string;
    name: string;
    placeholder: string;
    type: string;
    valide: () => boolean;
  };
}>();
const touched = ref(false);
const isError = computed(() => (touched.value ? !field.valide() : false));
</script>

<template>
  <div class="FormTextField">
    <label for="input-field"><slot></slot></label>
    <input
      :name="field.name"
      :type="field.type"
      id="input-field"
      :placeholder="field.placeholder"
      v-model="field.value"
      tabindex="1"
      @blur="touched = true"
    />
    <label v-if="isError" for="input-field" class="Error-label">
      Введено не корректное значение</label
    >
  </div>
</template>

<style lang="scss">
.FormTextField {
  padding: 8px;
}
label {
  display: block;
  font-size: 16px;
  color: #756f86;
}
#input-field {
  display: block;
  padding: 16px;
  margin-top: 7px;
  margin-bottom: 8px;
  font-size: 16px;
  width: 100%;
  height: 52px;
  border-radius: 6px;
  border: 1px solid #dbe2ea;
  box-shadow: 0px 4px 8px 0px #2c27380a;
  color: #2c2738;

  &:focus {
    border: 2px solid #0880ae;
  }
  &::placeholder {
    color: #7c9cbf;
  }
}
.Error-label {
  font-size: 14px;
  color: #ff7171;
}
</style>
