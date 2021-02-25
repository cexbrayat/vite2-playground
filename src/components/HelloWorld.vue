<template>
  <Form @submit="register($event)" v-slot="{ meta: formMeta }">
<Field name="password" rules="required" v-slot="{ field, meta }" v-model="user.password">
  <label for="password-input">Password</label>
  {{ meta }}
  <input id="password-input" type="password" :class="{ 'is-invalid': meta.dirty && !meta.valid }" v-bind="field" />
  <ErrorMessage name="password" class="error" />
</Field>
    <button :disabled="!formMeta.valid">Register</button>
  </Form>
  <!-- end::disabled-button[] -->
</template>

<script lang="ts">
/* eslint-disable no-console */
import { defineComponent, reactive } from 'vue';
import { ErrorMessage, Field, Form, defineRule, configure } from 'vee-validate';
import { confirmed, required } from '@vee-validate/rules';

defineRule('required', required);
defineRule('confirmed', confirmed);

configure({
  validateOnInput: true
})

export default defineComponent({
  name: 'HelloWorld',
  components: {
    ErrorMessage,
    Field,
    Form
  },
  setup() {
    const user = reactive({ password: '' });

    function register(values: any) {
      console.log(values);
    }

    return { user, register };
  }
});
</script>

<style scoped>
.is-invalid {
  border: 3px red solid;
}
</style>

