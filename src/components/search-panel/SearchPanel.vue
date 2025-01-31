<template>
    <div class="search-panel">
        <input 
            type="text" 
            placeholder="Sevimli kinolar"  
            v-model="searchQuery"
            @change="$emit('updateSearch', searchQuery)" 
        />
    </div>
</template>

<script>
export default {
    props: {
        initialQuery: String 
    },
    data() {
        return {
            searchQuery: this.initialQuery || '' 
        };
    },
    watch: {
        searchQuery(newQuery) {
            this.$emit('updateSearch', newQuery); 
        }
    }
}
</script>

<style scoped>
input {
    width: 100%;
    padding: 1.5rem;
    border: 1px solid #ccc;
    border-radius: 5px;
}
input::placeholder {
    font-size: 1rem;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}
</style>
