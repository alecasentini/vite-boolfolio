<script >

import ContactsForm from '../components/ContactsForm.vue';

export default {
    name: "Contact",
    components: {
        ContactsForm
    },

    data() {
        return {


        }
    },

    mounted() {

    },

    methods: {
        goBack() {
            this.$router.go(-1);
        },

    }

}
</script>

<template>
    <h1>Contatti</h1>
    <div class="container">
        <ContactsForm />
    </div>
    <a href="" @click.prevent="goBack" class="btn btn-primary mt-5">Go back</a>
</template>

<style lang="scss"></style>