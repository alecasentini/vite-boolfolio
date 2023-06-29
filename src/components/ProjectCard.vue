<script>


export default {
    name: "ProjectCard",

    props: ['elem'],
    data() {
        return {
            baseUrl: 'http://127.0.0.1:8000',
        }
    }
}
</script>

<template>
    <div class="card">
        <img class="card-img-top" :src="`${baseUrl}/storage/${elem.cover_image}`" alt="">
        <div class="card-body">
            <router-link :to="{ name: 'project', params: { slug: elem.slug } }">
                <h4 class="card-title">{{ elem.name }}</h4>
            </router-link>
            <p class="card-text">{{ elem.description }}</p>
            <div>
                <h5>Type</h5>
                <span v-if="elem.type">{{ elem.type.name }}</span>
            </div>
            <div>
                <h5>Technologies</h5>
                <ul v-if="elem.technologies">
                    <li v-for="(elem, index) in elem.technologies" :key="index">{{ elem.name }}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<style lang="scss"></style>