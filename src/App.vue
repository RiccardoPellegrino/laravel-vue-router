<template>
  <AppHeader></AppHeader>
  <div>
    <h1>{{titolo }}</h1>
    <ul>
      <li v-for="(project, index) in projects" :key="index">
        {{ project.slug }}
      </li>
    </ul>
  </div>
  <main>
    <route-view>
    </route-view>
  </main>
</template>

<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
export default {
  name:'App',
    data() {
        return {
            projects: [],
            urlApi: "http://localhost:8000/api",
            titolo: "Bel titolo"
        };
    },
    methods: {
        getProjects() {
            axios.get(`${this.urlApi}/projects`).then((response) => {
                console.log(response.data);
                this.projects = response.data.results.data;
            });
        }
    },
    computed: {},
    created() {
    },
    mounted() {
        this.getProjects();
    },
    beforeCreated() {
        // console.log("beforeCreated")
    },
    beforeUpdate() {
        // console.log("beforeUpdate")
    },
    update() {
        // console.log("Update")
    },
    components: { AppHeader }
}

</script>

<style lang="scss" scoped>

</style>