<script lang="ts">
import { PropType, defineComponent } from 'vue';

export default defineComponent({
    props: {
        activeFilter: {
            type: String as PropType<"All" | "Active" | "Done">,
            required: true
        }
    },
    data() {
        return {
            filters: ["All", "Active", "Done"]
        }
    },
    methods: {
        setFilter(filter: "All" | "Active" | "Done") {
            this.$emit('setFilter', filter)
        }
    },
    emits: {
        setFilter: (filter: "All" | "Active" | "Done") => filter
    }
})
</script>

<template>
    <aside class="app-filters">
        <section class="toggle-group">
            <button v-for="filter in filters" :key="filter" class="button" value="All" :class="{'button--primary' : activeFilter == filter}" @click="setFilter(filter)">{{ filter }}</button>
        </section>
    </aside>
</template>

<style></style>