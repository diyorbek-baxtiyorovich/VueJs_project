<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form d-flex" @submit.prevent="addMovie">
            <input 
                type="text" 
                class="form-control new-movie-label" 
                placeholder="Qaysi kino?"  
                v-model="name"
                required
            />
            <input 
                type="number" 
                class="form-control new-movie-label" 
                placeholder="Nechi marotaba ko'rilgan"  
                v-model.number="viewers"
                required
            />
            <button class="btn btn-outline-dark" type="submit">Qo'shish</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: '',
            viewers: ''
        };
    },
    methods: {
        addMovie() {
            if (this.name && this.viewers) {
                const newMovie = {
                    name: this.name,
                    viewers: this.viewers,
                    like: false,
                    favorite: false,
                    id: Date.now()
                };
                this.$emit('createMovie', newMovie);
                this.name = ''; 
                this.viewers = '';
            }
        }
    }
};
</script>

<style scoped>
.movie-add-form {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
}
</style>
