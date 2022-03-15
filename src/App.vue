<template>
  <form>
    <div>
      <input v-model="usernameValue" type="text" placeholder="Prénom" />
    </div>
    <pre>
 {{ errors }}
    </pre>
    <button @click="triggerErreur()">erreur</button>
    <button @click="triggerValue()">valeur</button>
  </form>
</template>

<script setup lang="ts">
import { useField, useForm } from 'vee-validate';
import { z } from 'zod';
import { toFieldValidator } from '@vee-validate/zod';

const {
  errors: formErrors,
  setFieldValue,
  setValues,
  setFieldError,
  setErrors: setFormErrors,
} = useForm();

const {
  value: usernameValue,
  errorMessage,
  errors,
  setValue,
  setErrors,
} = useField(
  'username',
  toFieldValidator(z.string().min(5, { message: 'Trop court !' }))
);

function triggerErreur() {
  setFieldError('username', 'oops');
}

function triggerValue() {
  setFieldValue('username', 'test');
}
</script>

<style scoped lang="scss"></style>
