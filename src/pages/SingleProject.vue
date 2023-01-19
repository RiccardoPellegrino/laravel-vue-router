<template>
    <section v-if="project">
        <h1>{{ project.name_project }}</h1>
        <img :src="`${store.imagBasePath}${project.cover_image}`" class="card-img-top" :alt="project.title">
        <p>{{ project.description }}</p>
        <div v-if="project.types">
            <h5>Type: {{ project.types.name }}</h5>
        </div>
        <div v-if="project.languages && project.languages.length > 0">
            <h5>Tags</h5>
            <div>
                <span v-for="(language, index) in project.languages" :key="index" class="badge text-bg-info">{{
                    language.name
                }}</span>
            </div>
        </div>
    </section>
    <section v-else>Loading...</section>
    <router-link class="btn btn-primary" :to="{ name: 'projects'}">
        Vedi il progetto
    </router-link>
</template>

<script>
import axios from 'axios';
import { store } from '../store';
export default {
    name: 'SingleProject',
    data() {
        return {
            store,
            project: null,
            currentPage: 1,
        }
    },
    methods: {
        getProject() {
            //  console.log(`${this.store.apiBaseUrl}/projects/${this.$route.params.slug}`);
            axios.get(`${this.store.apiBaseUrl}/projects/${this.$route.params.slug}`).then((response) => {

                console.log(response.data);
                if (response.data.succes) {
                    //  console.log('sono qui '+ response.data.results);
                    this.project = response.data.results;
                } else {
                    //console.log(this.$router);
                    this.$router.push({ name: 'not-found' });
                }

            });

        },
        prev() {
            if (this.currentPage > 1) {
                this.currentPage--;
                this.getProjects(this.currentPage)
            }
        },
    },
    mounted() {
        this.getProject();
    }

}
</script>

<style lang="scss" scoped>
img {
    max-width: 100px;
}
</style>