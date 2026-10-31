<script setup lang="ts">
import ContactForm from './components/ContactForm.vue';
</script>

<template>
    <main>
        <div class="container">
            <div class="row">
                <div class="col-12">
                    <h1 class="mb-4">Formulario de contacto</h1>
                    <ContactForm />
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped lang="scss">
main {
    background-color: #fafafa;
}
</style>
