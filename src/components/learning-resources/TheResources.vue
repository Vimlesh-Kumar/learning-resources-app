<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResourcesButton">Stored
            Resources</base-button>
        <base-button @click="setSelectedTab('add-resources')" :mode="AddResourcesButton">Add New
            Resource</base-button>
        <keep-alive>
            <component :is='selectedTab'></component>
        </keep-alive>
    </base-card>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResources from './AddResources.vue';

export default {
    components: {
        StoredResources,
        AddResources
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                {
                    id: 'angular',
                    title: 'Angular',
                    description: 'Angular is an application-design framework and development platform for creating efficient and sophisticated single-page apps.',
                    link: 'https://angular.io/docs'
                },
                {
                    id: 'vue',
                    title: 'Vue',
                    description: 'Vue (pronounced /vjuː/, like view) is a JavaScript framework for building user interfaces.',
                    link: 'https://vuejs.org/guide/introduction.html'
                }
            ]
        }
    },
    computed: {
        storedResourcesButton() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        AddResourcesButton() {
            return this.selectedTab === 'add-resources' ? null : 'flat';
        }
    },
    provide() {
        return {
            resources: this.storedResources,
            addResourceMethod: this.addResource,
            deleteResource:this.removeResource
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab
        },
        addResource(title, desciption, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: desciption,
                link: url
            }
            this.storedResources.unshift(newResource)
            this.selectedTab = 'stored-resources';
        },
        removeResource(resId){
            const resIndex=this.storedResources.findIndex(res=> res.id===resId)
            this.storedResources.splice(resIndex,1)
        }
    }
}
</script>