<script >
import axios from 'axios';

export default {
  data() {
    return {
      projects: [],
      baseUrl: 'http://127.0.0.1:8000',
      currentPage: 1,
      lastPage: null

    }
  },

  mounted() {
    this.getProjects(1);
  },

  methods: {
    getProjects(projectApiPage) {
      axios.get(`${this.baseUrl}/api/projects`, {
        params: {
          page: projectApiPage
        }
      })
        .then(res => {
          this.projects = res.data.projects.data
          this.currentPage = res.data.projects.current_page
          this.lastPage = res.data.projects.last_page
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

    <nav aria-label="Page navigation example" class="my-3">

      <ul class="pagination">

        <li class="page-item" style="cursor: pointer;"><a class="page-link" @click.prevent="getProjects(currentPage - 1)"
            href="#">Previous</a></li>

        <li class="page-item" style="cursor: pointer;" :class="(currentPage === elem) ? 'active' : ''"
          v-for="(elem, index) in lastPage" :key="index">
          <a class="page-link" @click.prevent="getProjects(elem)" href="#">
            {{ elem }}
          </a>
        </li>

        <li class="page-item" style="cursor: pointer;"><a class="page-link" @click.prevent="getProjects(currentPage + 1)"
            href="#">Next</a>
        </li>

      </ul>

    </nav>

  </div>
</template>

<style lang="scss">
@use './style/main.scss';
</style>
