<script setup lang="ts">
import { useForm } from 'vee-validate';
import * as yup from 'yup';

const schema = yup.object({
    name: yup
        .string()
        .required()
        .min(3)
        .max(100)
        .typeError('Mínimo de 3 caracteres. Máximo 100 caracteres.'),
    email: yup.string().required().email().typeError('Formato correcto.'),
    subject: yup.string().required().typeError('Debe escribir un asunto.'),
    message: yup.string().required().min(20).typeError('Mínimo 20 caracteres.'),
});

// Valores iniciales
const initialValues = {
    name: '',
    email: '',
    subject: '',
    message: '',
};

const { values, errors, meta, defineField } = useForm({ validationSchema: schema, initialValues });

// Campos
const [name, nameAtrrs] = defineField('name');
const [email, emailAtrrs] = defineField('email');
const [subject, subjectAtrrs] = defineField('subject');
const [message, messageAtrrs] = defineField('message');

// Submit simulado
const onSubmit = () => {
    console.log('REGISTER payload', JSON.stringify(values));
};
</script>

<template>
    <form class="card px-3 py-4 bg-white form-content" @submit.prevent="onSubmit">
        <div class="mb-2">
            <label for="name" class="mb-2 me-2">Nombre y apellidos:</label>
            <input
                type="text"
                v-model="name"
                name="name"
                id="name"
                v-bind="nameAtrrs"
                placeholder="Nombre"
                :class="{ invalid: !!errors.name }"
                :aria-invalid="!!errors.name"
                aria-describedby="name-error"
            />
            <p v-if="errors.name" id="name-error" class="error">{{ errors.name }}</p>
        </div>
        <div class="mb-2">
            <label for="email" class="mb-2 me-2">Email:</label>
            <input
                type="text"
                v-model="email"
                name="email"
                id="email"
                v-bind="emailAtrrs"
                placeholder="tu@email.com"
                :class="{ invalid: !!errors.email }"
                :aria-invalid="!!errors.email"
                aria-describedby="email-error"
            />
            <p v-if="errors.email" id="email-error" class="error">{{ errors.email }}</p>
        </div>
        <div class="mb-2">
            <label for="subject" class="mb-2 me-2">Asunto:</label>
            <input
                type="text"
                v-model="subject"
                name="subject"
                id="subject"
                v-bind="subjectAtrrs"
                placeholder=""
                :class="{ invalid: !!errors.subject }"
                :aria-invalid="!!errors.subject"
                aria-describedby="subject-error"
            />
            <p v-if="errors.subject" id="subject-error" class="error">{{ errors.subject }}</p>
        </div>
        <div class="mb-2">
            <label for="message" class="mb-2 me-2">Mensaje:</label>
            <textarea
                type="password"
                v-model="message"
                name="message"
                id="message"
                v-bind="messageAtrrs"
                placeholder=""
                :class="{ invalid: !!errors.message }"
                :aria-invalid="!!errors.message"
                aria-describedby="message-error"
            />
            <p v-if="errors.message" id="message-error" class="error">{{ errors.message }}</p>
        </div>

        <input type="submit" value="Enviar" class="mb-4 btn btn-primary" :disabled="!meta.valid" />
    </form>
</template>

<style scoped lang="scss">
pre {
    background-color: #fafafa;
}
.error {
    color: red;
}
#email:not(.invalid) {
    margin-bottom: 12px;
}
.invalid {
    outline: 1px solid red;
    border-radius: 2px;
}
</style>
