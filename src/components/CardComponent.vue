<template>
        <div class="my-card mt-5" style="width: 18rem;">
            <h1 class="text-center text-capitalize">{{ project.name_project }}</h1>
            <img :src="`${store.imagBasePath}${project.cover_image}`" class="card-img-top pt-3" :alt="project.title"
                v-if="(project.cover_image)">
            <img src="https://via.placeholder.com/100x100.png?text=Placeholder" class="card-img-top"
                :alt="project.title" v-else>
            <div class="my-card-body">
                <p class="card-text text-center mt-3"> <b>Descrizione:</b> <br> {{
                    truncateContent(project.description)
                }}</p>
                <div class="fondo">
                    <router-link class="btn btn-secondary"
                        :to="{ name: 'single-project', params: { slug: project.slug } }">
                        Vedi il progetto
                    </router-link>
                </div>
            </div>
        </div>
</template>

<script>
import { store } from '../store';
export default {
    name: 'CardComponent',
    data() {
        return {
            store
        }
    },
    methods: {
        truncateContent(text) {
            if (text.length > this.contentMaxLen) {
                return text.substr(0, this.contentMaxLen) + "...";
            }
            return text;
        }
    },
    props: ['project']

}
</script>

<style lang="scss" scoped>
.fondo {
    position: absolute;
    bottom: 0;
    left: 0;
}

.my-card {
    position: relative;
    box-shadow: 4px 8px rgba(235, 0, 0, 0.2);
    transition: 0.3s;
    width: 40%;
    background-color: beige;
    border-radius: 5px;
    height: 500px;
}

.my-card:hover {
    box-shadow: 0 12px 16px 0 rgba(195, 93, 226, 0.8);
}

.card-img-top {
    width: 100%;
    height: 10vw;
    object-fit: scale-down;
}

.btn-secondary {
    background-color: #805D93;
    border: none;
}

h1 {
    color: rgb(19, 192, 192);
}
</style>