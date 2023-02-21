<template>
    <Box>
        <p class="h2">Barcha kinolar soni: {{ allMoviesCount }}</p>
        <p class="h2">Ko'rilgan kinolar soni: {{ favouriteMoviesCount  }}</p>
    </Box>
</template>

<script>

export default {
    props:{
        allMoviesCount:{
            type: Number,
            required: true
        },
        favouriteMoviesCount:{
            type: Number,
            required: true
        }
    }
}
</script>

<style>
</style>