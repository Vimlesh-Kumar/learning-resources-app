<template>
    <ul>
        <learning-resource :id="resource.id" :title="resource.title" :description="resource.description" :link="resource.link"
            v-for="resource in resources" :key="resource.id"></learning-resource>
    </ul>
</template>

<script>
import learningResource from './LearningResource.vue'
export default {
    components: {
        learningResource
    },
    inject: ['resources']
}
</script>

<style scoped>
ul {
    list-style: none;
    margin: 0;
    padding: 0;
    margin: auto;
    max-width: 40rem;
}
</style>