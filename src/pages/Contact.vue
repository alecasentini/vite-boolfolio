<script >

export default {
    name: "Contact",
    components: {

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

    <a href="" @click.prevent="goBack" class="btn btn-primary">Go back</a>
</template>

<style lang="scss"></style>