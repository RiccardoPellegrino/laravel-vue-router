<template>
    <div class="text-center">
        <div class="d-flex justify-content-center align-items-center classe ">
            <section v-if="project">
                <div class="card text-center" style="width: 18rem;">
                    <h1>{{ project.name_project }}</h1>
                    <div class="d-flex justify-content-center">
                        <img :src="`${store.imagBasePath}${project.cover_image}`" class="card-img-top"
                            :alt="project.title">
                    </div>
                    <p>{{ project.description }}</p>
                    <div v-if="project.types">
                        <h5>Type: {{ project.types.name }}</h5>
                    </div>
                    <div v-if="project.languages && project.languages.length > 0">
                        <h5>Tags</h5>
                        <div class="mt-3 mb-3">
                            <span v-for="(language, index) in project.languages" :key="index"
                                class="badge text-bg-info">{{
                                    language.name
                                }}</span>
                        </div>
                    </div>
                    <div>
                        <router-link class="btn btn-secondary" :to="{ name: 'projects' }">
                            Indietro
                        </router-link>
                    </div>
                </div>
            </section>
            <section v-else>Loading...</section>
        </div>

    </div>
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

.classe {
    min-height: 80vh;
}
.btn-secondary {
    background-color: #805D93;
    border: none;
}
</style>