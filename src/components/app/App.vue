<template>
    <div class="app">
        <div class="content">
            <AppInfo 
                :addMovieCount="movies.length" 
                :favMovieCount="movies.filter(c => c.favorite).length"  
            />
            <div class="search-panel-wrapper">
                <SearchPanel @updateSearch="updateSearchQuery" />
                <AppFilter />
            </div>
            <MovieList 
                :movies="filteredMovies"  
                @onLike="onLikeHandel" 
                @onFavourite="onFavouriteHandel" 
                @onDelete = "onDeleteHandel"
            /> 
            <MovieAddForm @createMovie="addMovie" />
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import AppFilter from '../app-filter/AppFilter.vue';
import AppInfo from '../app-info/AppInfo.vue';
import MovieAddForm from '../movie-add-form/MovieAddForm.vue';
import MovieList from '../movie-list/MovieList.vue';
import SearchPanel from '../search-panel/SearchPanel.vue';

export default {
    components: {
        AppInfo,
        SearchPanel,
        AppFilter,
        MovieList,
        MovieAddForm
    },
    data() {
        return {
            movies: [],
            searchQuery: ''
        };
    },
    computed: {
        filteredMovies() {
            return this.movies.filter(movie => 
                movie.name.toLowerCase().includes(this.searchQuery.toLowerCase())
            );
        }
    },
    methods: {
        addMovie(newMovie) {
            this.movies.push(newMovie);
        }, 
        updateSearchQuery(query) {
            this.searchQuery = query;
        },
        onLikeHandel(id) {
            this.movies = this.movies.map(item => 
                item.id === id ? { ...item, like: !item.like } : item
            );
        },
        onFavouriteHandel(id) {
            this.movies = this.movies.map(item => 
                item.id === id ? { ...item, favorite: !item.favorite } : item
            );
        },
        onDeleteHandel(id){
            this.movies = this.movies.filter(c => c.id !== id)
        },
        async fetchMovie(){
            const {data} = await axios.get("https://jsonplaceholder.typicode.com/posts?_limit=10");
            const newArr = data.map(item => ({
                id: item.id,
                name: item.title,
                like: false,
                favorite: false,
                viewers: item.id * 10
            }))
            this.movies = newArr
        }
    },
    mounted(){
        this.fetchMovie()
    }
}
</script>

<style>
.app {
    width: 100%;
    height: auto;
    background-color: aqua;
}

.content {
    width: 1000px;
    min-height: 700px;
    margin: 0 auto;
    padding: 5rem 0;
}

.search-panel-wrapper {
    background-color: #f4f4f4;
    padding: 1rem;
    border-radius: 5px;
    margin-bottom: 1rem;
}
</style>