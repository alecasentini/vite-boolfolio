<script >
import axios, { all } from 'axios';

export default {
    name: "ContactsForm",
    components: {

    },

    data() {
        return {
            name: '',
            email: '',
            message: '',
            baseUrl: 'http://127.0.0.1:8000',
            success: false,
            errors: {}

        }
    },
    methods: {
        sendForm() {
            const data = {
                name: this.name,
                email: this.email,
                message: this.message,
            }

            axios.post(`${this.baseUrl}/api/contacts`, data).then(res => {
                this.success = res.data.success
                if (this.success) {
                    this.name = '';
                    this.email = '';
                    this.message = '';
                } else {
                    this.errors = res.data.errors;
                }
            })
        }
    }

}
</script>

<template>
    <div>
        <h2>Contact Form</h2>
        <form @submit.prevent="sendForm()">
            <div class="mb-3">
                <label for="" class="form-label">Name</label>
                <input v-model="name" type="text" class="form-control" name="name" id="" aria-describedby="helpId"
                    placeholder="Inserisci il tuo nome">
            </div>

            <div class="mb-3">
                <label for="" class="form-label">Email</label>
                <input v-model="email" type="email" class="form-control" name="email" id="" aria-describedby="helpId"
                    placeholder="Inserisci la tua email">
            </div>

            <div class="mb-3">
                <label for="" class="form-label">Message</label>
                <textarea v-model="message" class="form-control" name="message" id="" rows="3"
                    placeholder="Scrivi il testo del messaggio"> </textarea>
            </div>

            <button type="submit" class="btn btn-primary">
                Invia
            </button>
        </form>

    </div>
</template>

<style lang="scss"></style>