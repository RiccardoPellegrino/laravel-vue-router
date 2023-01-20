<template>
    <section>
        <h1>Lista dei progetti</h1>
        <div class="row">
            <div class="col-12 col-md-4 mt-5" v-for="(project, index) in projects" :key="index">
                <CardComponent :project="project"/>
            </div>
        </div>
        <nav aria-label="Page navigation example">
            <ul class="pagination mt-5">
                <li class="page-item"><a class="page-link" href="#">Previous</a></li>
                <li class="page-item" v-for="n in lastPage"><a class="page-link" @click="getProjects(n)">{{ n }}</a></li>
            </ul>
        </nav>
    </section>
</template>

<script>
import axios from 'axios';
import CardComponent from '../components/CardComponent.vue';
import { store } from '../store';
export default {
    name: "ProjectList",
    components:{CardComponent},
    data() {
        return {
            store,
            projects: [],
            currentPage: 1,
            lastPage: null,
            total: 0,
            contentMaxLen: 100
        };
    },
    methods: {
        getProjects(pagenum) {
            axios.get(`${this.store.apiBaseUrl}/projects`, {
                params: {
                    page: pagenum
                }
            }).then((response) => {
                //console.log(response.data.results);
                this.projects = response.data.results.data;
                this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
                this.total = response.data.results.total;
            });
        },
        truncateContent(text) {
            if (text.length > this.contentMaxLen) {
                return text.substr(0, this.contentMaxLen) + "...";
            }
            return text;
        }
    },
    mounted() {
        this.getProjects(1);
    },
    components: { CardComponent }
}
</script>

<style lang="scss" scoped>
.card {
    height: 600px;
}
</style>