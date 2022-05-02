<template>
    <base-layout :page-title="memory ? memory.title : 'Loging ...'" page-default-back-link="/memories">
        <h2 v-if="!memory">Could not found a memory for the given Id.</h2>
        <memory-overview
            v-else
            :title="memory.title"
            :image="memory.image"
            :description="memory.description"
        ></memory-overview>
    </base-layout>
</template>

<script>
import MemoryOverview from '../components/memories/MemoryOverview.vue'

export default {
    components:{
        MemoryOverview
    },
    data(){
        return {
            memoryId: this.$route.params.id,
        }
    },
    computed:{
        memory() {
            return this.$store.getters.memory(this.memoryId);
        }
    }
}
</script>

<style>

</style>