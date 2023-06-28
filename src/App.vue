<script >
import axios from 'axios';

export default {
  data() {
    return {
      projects: [],
      baseUrl: 'http://127.0.0.1:8000'

    }
  },

  mounted() {
    this.getProjects();
  },

  methods: {
    getProjects() {
      axios.get(`${this.baseUrl}/api/projects`)
        .then(res => {
          this.projects = res.data.projects
        })
    }
  }

}
</script>

<template>
  <h1>Projects</h1>

  <div class="container">
    <div class="row">
      <div class="col-6 " v-for="(elem, index) in  projects " :key="index">
        <div class="card">
          <img class="card-img-top" :src="`${baseUrl}/storage/${elem.cover_image}`" alt="">
          <div class="card-body">
            <h4 class="card-title">{{ elem.name }}</h4>
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
      </div>
    </div>

  </div>
</template>

<style lang="scss">
@use './style/main.scss';
</style>
