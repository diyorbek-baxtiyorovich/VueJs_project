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
            movies: [
                { name: "Keybda", viewers: 542, like: true, favorite: false, id: 1 },
                { name: "Samobo", viewers: 513, like: false, favorite: true, id: 2 },
                { name: "Direktsv", viewers: 123, like: false, favorite: false, id: 3 }
            ],
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
        }
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