<template>
    <div class="app">
        <div class="content">
            <AppInfo 
                :allMoviesCount="movies.length"
                :favouriteMoviesCount="movies.filter(c => c.favourite).length"
            />

            <div class="search-panel">
                <SearchPanel/>
                <AppFilter/>
            </div>

            <MovieList :movies="movies"/>
            <MovieAddForm />
        </div>
    </div>
</template>

<script>

import AppInfo from '@/components/app-info/AppInfo.vue';
import SearchPanel from '@/components/search-panel/SearchPanel.vue';
import AppFilter from '@/components/app-filter/AppFilter.vue';
import MovieList from '@/components/movie-list/MovieList.vue';
import MovieAddForm from '@/components/movie-add-form/MovieAddForm.vue';

export default{
    components: {
        AppInfo,
        SearchPanel,
        AppFilter,
        MovieList,
        MovieAddForm
    },
    data(){
        return {
            movies: [
                {
                    name: 'Omar',
                    viewers: 811,
                    favourite: false,
                    like: true
                },
                {
                    name: 'Omar 46a ',
                    viewers: 13,
                    favourite: false,
                    like: false
                },
                {
                    name: 'Kelajak 456',
                    viewers: 12,
                    favourite: false,
                    like: false
                },
                {
                    name: 'A4465 Kuni',
                    viewers: 3232,
                    favourite: false,
                    like: false
                },
                {
                    name: 'Nima gapla?',
                    viewers: 787,
                    favourite: true,
                    like: false
                },
                {
                    name: 'Nima gapla?',
                    viewers: 787,
                    favourite: false,
                    like: false
                },
            ]
        }
    }
}
</script>

<style>
.app{
    height: 100vh;
    color: #000;
}

.content{
    width: 1000px;
    min-height: 700px;
    background-color: #fff;
    margin: 0 auto;
    padding: 5rem 0;
}

.search-panel{
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>