<template>
<ul>
    <resources-item v-for="resource in resources" :key="resource.id" :id="resource.id" :title="resource.title" :description="resource.description" :link="resource.link"></resources-item>
</ul>
</template>

<script>
import ResourcesItem from "./ResourceItem.vue";

export default {
    components: {
        ResourcesItem,
    },
    inject: ["resources"],
};
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
