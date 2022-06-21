<template>
  <form @submit.prevent="submitForm" class="create-profile-form">
    <label for="name">
      <div class="create-profile-form__container">
        <span class="create-profile-form__text-label">Name:</span>
        <input
          v-model="form.name"
          type="text"
          id="name"
          class="create-profile-form__input"
        />
      </div>
      <span class="error" v-if="errorFields.name?.length">{{
        errorFields.name[0].message
      }}</span>
    </label>

    <label for="email">
      <div class="create-profile-form__container">
        <span class="create-profile-form__text-label">Email :</span>
        <input
          v-model="form.email"
          type="text"
          id="email"
          class="create-profile-form__input"
        />
      </div>
      <span class="error" v-if="errorFields.email?.length">{{
        errorFields.email[0].message
      }}</span>
    </label>

    <label for="Specialisation">
      <div class="create-profile-form__container">
        <span class="create-profile-form__text-label">Specialisation: </span>

        <select
          v-model="form.specialisation"
          id="Specialisation"
          name="Specialisation"
          class="create-profile-form__select-input"
        >
          <option value="Surgeon">Surgeon</option>
          <option value="Radiologist">Radiologist</option>
          <option value="Cardiologist">Cardiologist</option>
          <option value="Psychiatrist">Psychiatrist</option>
          <option value="Dermatologist">Dermatologist</option>
        </select>
      </div>
      <span class="error" v-if="errorFields.specialisation?.length">
        {{ errorFields.specialisation[0].message }}</span
      >
    </label>

    <button
      type="submit"
      :disabled="!pass"
      class="create-profile-form__submit-btn"
    >
      Submit
    </button>
  </form>
</template>

<script setup>
import { reactive } from "vue";
import { useAsyncValidator } from "@vueuse/integrations/useAsyncValidator";

const rules = {
  name: {
    type: "string",
    required: true,
    validator: (rule, value) => /^[a-zA-Z\s]+$/.test(value),
    message: "Name must be only English letters",
  },
  email: [
    {
      type: "email",
      required: true,
    },
  ],
  specialisation: {
    type: "string",
    required: true,
  },
};

const form = reactive({
  name: "",
  email: "",
  specialisation: "",
});

const { pass, isFinished, errorFields } = useAsyncValidator(form, rules);

const emit = defineEmits(["submitForm"]);

function submitForm() {
  if (!isFinished.value) return;

  emit("submitForm", form);
}
</script>

<style src="./index.scss" lang="scss" scoped />
