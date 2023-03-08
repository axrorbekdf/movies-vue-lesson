<template>
    <div class="app">
        <div class="content">
            <AppInfo 
                :allMoviesCount="movies.length"
                :favouriteMoviesCount="movies.filter(c => c.favourite).length"
            />

            <div class="search-panel">
                <SearchPanel 
                    :updateTermHandler="updateTermHandler"
                />
                <AppFilter 
                    :updateFilterHandler="updateFilterHandler" :filterName="filter"
                />
            </div> 

            

            <Box 
                v-if="!movies.length && !isLoading"
            >
                <p class="fs-4 text-center text-danger">Kinolar mavjud emas!</p>
            </Box>

            <Box 
                v-else-if="isLoading"
                class="d-flex justify-content-center"
            >
                <Loader/>
            </Box>

            <div v-else>
                <Box>
                        <Pagination 
                            :pageCount="totalPages" 
                            :activePage="page" 
                            :changePage="changePageHandler"/>
                </Box>
                <MovieList 
                    style="margin-top: 0; padding-top: 0"
                    :movies="onFilterHandler(onSearchHandler(movies, term), filter)" 
                    @onToggle="toggleHandler" 
                    @onRemove = "onRemoveHandler"
                />
            </div>
           

            

            <MovieAddForm @createMovie="createMovie" />
        </div>
    </div>
</template>

<script>

import AppInfo from '@/components/app-info/AppInfo.vue';
import SearchPanel from '@/components/search-panel/SearchPanel.vue';
import AppFilter from '@/components/app-filter/AppFilter.vue';
import MovieList from '@/components/movie-list/MovieList.vue';
import MovieAddForm from '@/components/movie-add-form/MovieAddForm.vue';
import Pagination from '@/components/pagination/Pagination.vue';
import axios from "axios";

export default{
    components: {
        AppInfo,
        SearchPanel,
        AppFilter,
        MovieList,
        MovieAddForm,
        Pagination,
    },
    data(){
        return {
            movies: [],
            term: '',
            filter: 'all',
            isLoading: false,
            limit: 10,
            page: 1,
            totalPages: 0
        }
    },
    mounted(){
        this.fetchMovies()
    },
    watch: {
        page(){
            this.fetchMovies()
        }
    },
    methods:{
        createMovie(data){
            this.movies.push(data)
        },
        onRemoveHandler(id){
            this.movies = this.movies.filter(c => c.id != id);
        },
        toggleHandler(data){

            this.movies = this.movies.map(item => {
                if(item.id == data.id){
                    return {...item, [data.prop]: !item[data.prop]}
                }
                return item
            })
        },
        onSearchHandler(arr, term){

            if(arr.length == 0){
                return arr;
            }

            return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1);
        },

        onFilterHandler(arr, filter){
            switch (filter) {
                case 'popular':
                    return arr.filter(c => c.like)
                case 'mostViewers':
                    return arr.filter(c => c.viewers > 500)
                default:
                    return arr;
            }
        },
        updateTermHandler(term){
            this.term = term
        },
        updateFilterHandler(filter){
            this.filter = filter
        },

        
        async fetchMovies(){

            try{
                this.isLoading = true;

                const response = await axios.get("https://jsonplaceholder.typicode.com/posts", {
                    params: {
                        _limit: this.limit,
                        _page: this.page,
                    }
                })

                const newArr = response.data.map(item => ({
                    id: item.id,
                    name: item.title,
                    viewers: item.id*10,
                    favourite: false,
                    like: false
                }))
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
                this.movies = newArr;
            }catch(error){
                alert(error.message)
            } finally {
                this.isLoading = false;
            }
        },
        changePageHandler(page){
            this.page = page
        },

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
}

.search-panel{
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>