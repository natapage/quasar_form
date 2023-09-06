<script setup lang="ts">
import { ref } from 'vue';

const requiredRule = (val: string) =>
  (val && val.length > 0) || 'Please type something';

const form = ref({
  title: '',
  body: '',
  accepted: false,
});

const initialFormState = { ...form.value };

function onSubmit(event: Event) {
  const target = event.target as HTMLFormElement;
  if (!form.value.accepted) {
    return;
  }
  target.submit();
}

function onReset() {
  // Сбрасываем значения формы к начальному состоянию
  Object.assign(form.value, initialFormState);
}
</script>

<template>
  <q-page class="flex flex-center">
    <q-form
      class="column q-pa-md shadow-2"
      action="http://localhost:9000/"
      method="GET"
      @submit="onSubmit"
    >
      <q-input
        name="title"
        placeholder="Post Title"
        v-model="form.title"
        :rules="[requiredRule]"
      />
      <q-input
        type="textarea"
        name="body"
        placeholder="Your post.."
        v-model="form.body"
        :rules="[requiredRule]"
      />
      <q-toggle
        style="margin-top: 10px"
        v-model="form.accepted"
        label="I accepted license and terms"
      />

      <q-btn label="Submit" type="submit" color="indigo" />
      <q-btn label="Reset" type="reset" flat @click="onReset" />
    </q-form>
  </q-page>
</template>
