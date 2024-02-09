<script setup lang="ts">
import { toTypedSchema } from '@vee-validate/yup';
import { useForm } from 'vee-validate';
import { ObjectSchema, number, object, string } from 'yup';

interface User {
  id?: number;
  fullName: string;
}

const schema = toTypedSchema<ObjectSchema<User>>(
  object({
    id: number().optional(),
    fullName: string().required(),
  })
);

const { errors, defineField, handleSubmit } = useForm({
  validationSchema: schema,
});

const onSubmit = handleSubmit((values) => {
  console.log(values);
})

const [id] = defineField('id');
const [fullName] = defineField('fullName');
</script>

<template>
  <form @submit.prevent="onSubmit">
    <input type="number" v-model="id">
    <input type="text" v-model="fullName">
    <input type="submit">
  </form>
  <pre>{{ errors }}</pre>
</template>