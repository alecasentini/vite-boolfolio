<script >
import axios from 'axios';
import ProjectCard from './components/ProjectCard.vue';

export default {
  name: "App",
  components: {
    ProjectCard
  },

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
    getProjects(projectApiPage, prevPage, nextPage) {
      if (prevPage && this.currentPage === 1) {
        projectApiPage = this.lastPage;
      } else if (nextPage && this.currentPage === this.lastPage) {
        projectApiPage = 1;
      }
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
        <ProjectCard :elem="elem" />
      </div>
    </div>

    <nav aria-label="Page navigation example" class="my-3">

      <ul class="pagination">

        <li class="page-item" style="cursor: pointer;">
          <a class="page-link" @click.prevent="getProjects(currentPage - 1, true)" href="#">Previous</a>
        </li>

        <li class="page-item" style="cursor: pointer;" :class="(currentPage === elem) ? 'active' : ''"
          v-for="(elem, index) in lastPage" :key="index">
          <a class="page-link" @click.prevent="getProjects(elem)" href="#">
            {{ elem }}
          </a>
        </li>

        <li class="page-item" style="cursor: pointer;">
          <a class="page-link" @click.prevent="getProjects(currentPage + 1, false, true)" href="#">Next</a>
        </li>

      </ul>

    </nav>

  </div>
</template>

<style lang="scss">
@use './style/main.scss';
</style>
