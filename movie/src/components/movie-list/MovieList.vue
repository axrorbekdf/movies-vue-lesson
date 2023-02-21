<template>
    <div class="mt-5">
        <ul class="list-group list-group-flush">
           <MovieListItem v-for="movie in movies" :key="movie.id" :movie="movie" @onToggle="$emit('onToggle', $event)" @onRemove="$emit('onRemove', $event)"/>
        </ul>
    </div>
</template>

<script>
import MovieListItem from '../movie-list-item/MovieListItem.vue';

export default{
    components: {
        MovieListItem,
    },
    props:{
        movies:{
            type: Array,
            required: true
        }
    }
}
</script>