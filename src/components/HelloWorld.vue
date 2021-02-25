<template>
  <Form @submit="register($event)" v-slot="{ meta: formMeta }">
    <Field name="password" rules="required" v-slot="{ field }" v-model="user.password">
      <label for="password-input">Password</label>
      <input id="password-input" type="password" v-bind="field" />
      <ErrorMessage name="password" class="error" />
    </Field>
    <Field
      name="confirmPassword"
      rules="required|confirmed:@password"
      label="password confirmation"
      v-slot="{ field }"
      v-model="user.confirmPassword"
    >
      <label for="confirm-password-input">Confirm password</label>
      <input
        id="confirm-password-input"
        type="password"
        v-bind="field"
      />
      <ErrorMessage name="confirmPassword" class="error" />
    </Field>
    <button :disabled="!formMeta.dirty || !formMeta.valid">Register</button>
  </Form>
  <!-- end::disabled-button[] -->
</template>

<script lang="ts">
/* eslint-disable no-console */
import { defineComponent, reactive } from 'vue';
import { ErrorMessage, Field, Form, defineRule } from 'vee-validate';
import { confirmed, required } from '@vee-validate/rules';

defineRule('required', required);
defineRule('confirmed', confirmed);

export default defineComponent({
  name: 'HelloWorld',
  components: {
    ErrorMessage,
    Field,
    Form
  },
  setup() {
    const user = reactive({ password: '', confirmPassword: '' });

    function register(values: any) {
      console.log(values);
    }

    return { user, register };
  }
});
</script>
