<template>
    <ul class="movie-list list-group">
        <MovieListItem 
            v-for="movie in movies" 
            :key="movie.id"
            :movie="movie" 
            @onLike="$emit('onLike', movie.id)" 
            @onFavourite="$emit('onFavourite', movie.id)" 
            @onDelete = "$emit('onDelete', $event)"
        />
    </ul>
</template>

<script>
import MovieListItem from '../movie-list-item/MovieListItem.vue';

export default {
    components: {
        MovieListItem
    },
    props: {
        movies: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
.movie-list {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
}
</style>
