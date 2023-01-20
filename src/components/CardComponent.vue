<template>
    <div class="card position-static" style="width: 18rem;">
        <img :src="`${store.imagBasePath}${project.cover_image}`" class="card-img-top mt-3" :alt="project.title"
            v-if="(project.cover_image)">
        <img src="https://via.placeholder.com/100x100.png?text=Placeholder" class="card-img-top" :alt="project.title"
            v-else>
        <div class="card-body">
            <h5 class="card-title">{{ project.title }}</h5>
            <p class="card-text">{{ truncateContent(project.description) }}</p>
            <div class="fondo">
                <router-link class="btn btn-primary" :to="{ name: 'single-project', params: { slug: project.slug } }">
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
.fondo{
 position: absolute;
 bottom: 0;
 left: 0;
}
</style>