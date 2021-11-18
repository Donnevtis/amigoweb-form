<script setup lang="ts">
import { ref, computed } from "vue";

const { field } = defineProps<{
  field: {
    value: string;
    name: string;
    placeholder: string;
    options: string[];
    validators: ((str: any) => boolean)[];
    valide: () => boolean;
  };
}>();

const { name, options, placeholder } = field;
const selectedOption = ref(placeholder);
const listIsShown = ref(false);
const isSelected = ref(null);

function setOption(option) {
  selectedOption.value = option;
  isSelected.value = true;
}

function showList(e) {
  if (listIsShown.value === true) return;
  listIsShown.value = true;
  e.stopPropagation();
  document.addEventListener("click", hideList);
}

function hideList() {
  listIsShown.value = false;
  document.removeEventListener("click", hideList);
}
function toggleList(e) {
  !listIsShown.value ? showList(e) : hideList();
}

const touched = ref(false);
const isError = computed(() => (touched.value ? !field.valide() : false));
</script>

<template>
  <div class="FormDropdown">
    <label class="FormDropdown-label" :for="name">{{ placeholder }}</label>
    <div class="FormDropdown__container" @keyup.enter="toggleList" tabindex="1">
      <input
        class="FormDropdown__button"
        type="button"
        :name="name"
        :id="name"
        @click="showList"
        :class="{
          FormDropdown__button_selected: isSelected,
        }"
        :value="selectedOption"
        @blur="touched = true"
      />
      <ul
        v-show="listIsShown"
        @select-option="setOption"
        class="FormDropdown__list"
      >
        <li
          v-for="option in options"
          class="FormDropdown__list__Item"
          @click="
            setOption(option);
            $emit('update:modelValue', selectedOption);
          "
          @keyup.enter="
            setOption(option);
            $emit('update:modelValue', selectedOption);
          "
          tabindex="2"
        >
          <span>{{ option }}</span>
        </li>
      </ul>
    </div>
    <label v-if="isError" for="input-field" class="Error-label">
      Введено не корректное значение</label
    >
  </div>
</template>

<style scoped lang="scss">
.FormDropdown {
  position: relative;
  padding: 8px;
  outline: none;
  &-label {
    display: block;
    font-size: 16px;
    color: #756f86;
  }
  &__button {
    display: block;
    padding: 16px;
    margin-top: 7px;
    margin-bottom: 4px;
    font-size: 16px;
    width: 100%;
    border-radius: 6px;
    border: 1px solid #dbe2ea;
    box-shadow: 0px 4px 8px 0px #2c27380a;
    color: #7c9cbf;
    background-image: url("../../assets/svg/Chevron_Bottom.svg");
    background-repeat: no-repeat;
    background-position: 97% center;
    text-align: left;

    &_selected {
      color: #2c2738;
    }
  }
  &__container:focus .FormDropdown__button {
    border: 2px solid #0880ae;
    color: #2c2738;
  }
  &__list {
    position: absolute;
    left: 0;
    right: 0;
    border: 1px solid #dbe2ea;
    border-radius: 6px;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04),
      0px 20px 20px rgba(44, 39, 56, 0.04);
    overflow: hidden;
    background-color: #fff;
    z-index: 2;
    &__Item {
      height: 44px;
      display: flex;
      align-items: center;
      padding-left: 16px;
      color: #756f86;
      cursor: pointer;
      &:hover,
      &:focus {
        background: #ebf4f8;
      }
    }
    margin: 0 8px 0 8px;
  }
}
.Error-label {
  font-size: 14px;
  color: #ff7171;
}
</style>
