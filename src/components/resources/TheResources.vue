<template>
<base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resources')" :mode="addResButtonMode">Add Resources</base-button>
</base-card>
<keep-alive>
    <component :is="selectedTab"></component>
</keep-alive>
</template>

<script>
import StoredResources from "./StoredResources.vue";
import AddResources from "./AddResources.vue";

export default {
    components: {
        StoredResources,
        AddResources,
    },
    data() {
        return {
            selectedTab: "stored-resources",
            storedResources: [{
                    id: "facebook",
                    title: "Facebook",
                    description: "Text",
                    link: "https://facebook.com",
                },
                {
                    id: "google",
                    title: "Google",
                    description: "Text",
                    link: "https://google.com",
                },
            ],
        };
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource,
        };
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === "stored-resources" ? null : "flat";
        },
        addResButtonMode() {
            return this.selectedTab === "add-resources" ? null : "flat";
        },
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, discription, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                discription: discription,
                link: url,
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = "stored-resources";
        },
        removeResource(resId) {
            const resIndex = this.storedResources.findIndex(
                (resource) => resource.id === resId
            );
            this.storedResources.splice(resIndex, 1);
        },
    },
};
</script>

<style>
</style>
