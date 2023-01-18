<template>
  <div>
    <h1>{{titolo }}</h1>
    <ul>
      <li v-for="(project, index) in projects" :key="index">
        {{ project.slug }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      projects: [],
      urlApi:'http://localhost:8000/api',
      titolo:'Bel titolo'
    }
  },
    methods: {
      getProjects(){
        axios.get(`${this.urlApi}/projects`).then((response)=>{
          console.log(response.data);
        this.projects = response.data.results.data;
        })
      }

  },
  computed: {

  },

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
  }

}

</script>

<style lang="scss" scoped>

</style>