<script >
import axios from 'axios';
import ProjectCard from '../components/ProjectCard.vue';

export default {
    name: "SingleProject",
    components: {
        ProjectCard
    },

    data() {
        return {

            baseUrl: 'http://127.0.0.1:8000',
            project: null
            // currentPage: 1,
            // lastPage: null

        }
    },

    created() {
        // this.getProjects(1);
        this.getSingleProject();
    },

    methods: {

        getSingleProject() {
            axios.get(`${this.baseUrl}/api/projects/${this.$route.params.slug}`).then((response) => {
                if (response.data.success) {
                    this.project = response.data.project;
                } else {
                    // redirect alla pagina 404
                    this.$router.push({ name: 'not-found' })
                }
            });
        }
        // getProjects(projectApiPage, prevPage, nextPage) {
        //     if (prevPage && this.currentPage === 1) {
        //         projectApiPage = this.lastPage;
        //     } else if (nextPage && this.currentPage === this.lastPage) {
        //         projectApiPage = 1;
        //     }
        //     axios.get(`${this.baseUrl}/api/projects`, {
        //         params: {
        //             page: projectApiPage
        //         }
        //     })
        //         .then(res => {
        //             this.projects = res.data.projects.data
        //             this.currentPage = res.data.projects.current_page
        //             this.lastPage = res.data.projects.last_page
        //         })
        // }
    }

}
</script>

<template>
    <h1>Single Project: {{ project.name }} </h1>
    <img class="w-50" :src="`${baseUrl}/storage/${project.cover_image}`" alt="">
    <p>Descrizione: {{ project.description }}</p>

    <p>Type: {{ project.type.name }}</p>

    <p>Technologies:
        <span v-for="(elem, index) in project.technologies" :key="index" class="me-2">{{ elem.name }} </span>
    </p>
</template>

<style lang="scss"></style>