<script setup lang="ts">
import { ref, reactive, computed } from "vue";
import FormField from "./inputs/FormTextField.vue";
import FormSelect from "./inputs/FormDropdown.vue";
import FormCheckbox from "./inputs/FormCheckbox.vue";
import FormSubmit from "./inputs/FormLargeButton.vue";

const singupLink = ref("#");
const termsLink = ref("#");

const onlyLetters = str =>
  /^[a-zA-Z]+(([',. -][a-zA-Z ])?[a-zA-Z]*)*$/g.test(str);
const isEmail = str =>
  /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
    str,
  );
const length = len => str => str.length >= len;
const isPhone = str =>
  /^[+]*[(]{0,1}[0-9]{1,4}[)]{0,1}[-\s\./0-9]*$/g.test(str);

function valide() {
  return !this.validators.find(validator => !validator(this.value));
}

const fields = {
  username: {
    value: "",
    type: "text",
    name: "Имя",
    placeholder: "Введите ваше имя",
    validators: [onlyLetters],
    valide,
  },
  email: {
    value: "",
    type: "email",
    name: "Email",
    placeholder: "Введите ваше email",
    validators: [isEmail],
    valide,
  },
  phone: {
    value: "",
    type: "tel",
    name: "Номер телефона",
    placeholder: "Введите номер телефона",
    validators: [length(11), isPhone],
    valide,
  },
  language: {
    value: "",
    name: "language",
    placeholder: "Язык",
    options: ["Русский", "Английский", "Китайский", "Испанский"],
    validators: [length(3)],
    valide,
  },
  terms: {
    value: false,
    type: "checkbox",
    validators: [_ => _],
    valide,
  },
};

const form = reactive(fields);
const legal = computed(() => !Object.values(form).find(el => !el.valide()));
</script>

<template>
  <section class="FormLayout">
    <header class="FormLayout__header">
      <h1 class="Head1">Регистрация</h1>
      <p class="SingupHint">
        Уже есть аккаунт?
        <a :href="singupLink" class="FormLink">Войти</a>
      </p>
    </header>
    <section class="FormLayout__content">
      <form @submit.prevent>
        <FormField :field="form.username" v-model.trim="form.username.value">{{
          form.username.name
        }}</FormField>
        <FormField :field="form.email" v-model.trim="form.email.value">{{
          form.email.name
        }}</FormField>
        <FormField :field="form.phone" v-model="form.phone.value">{{
          form.phone.name
        }}</FormField>
        <FormSelect
          :field="form.language"
          v-model="form.language.value"
        ></FormSelect>
        <FormCheckbox v-model="form.terms.value">
          <span class="FromConsest">
            Принимаю
            <a :href="termsLink" class="FormLink">условия</a> использования
          </span>
        </FormCheckbox>
        <FormSubmit
          value="Зарегистрироваться"
          type="submit"
          :disabled="!legal"
        />
      </form>
    </section>
  </section>
</template>

<style scoped lang="scss">
.FormLayout {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 30px;
  height: 789px;
  max-width: 460px;
  min-width: 360px;
  border-radius: 24px;
  background: #fff;
  box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.02),
    0px 32px 64px rgba(44, 39, 56, 0.04);
  .FormLayout__header {
    display: block;
    margin: 0;
    width: 100%;
  }
  .FormLayout__content {
    height: 100%;
    margin-top: 56px;

    & form {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      height: 100%;
    }
  }
}

.FromConsest,
.SingupHint {
  font-family: IBM Plex Sans;
  font-size: 16px;
  font-weight: 500;
  color: #756f86;
}
.FormLink {
  color: #0880ae;
}
</style>
