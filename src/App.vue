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

const { defineField } = useForm({
  validationSchema: schema,
});

const [id] = defineField('id');
const [fullName] = defineField('fullName');
</script>
