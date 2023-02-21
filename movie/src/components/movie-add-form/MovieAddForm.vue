<template>
    <div class="pt-3">
        <h1 class="h3">Yangi kino qo'shish</h1>
        <form action="" class="d-flex" @submit.prevent>
            <input type="text" class="form-control" placeholder="Qanday kino?"
                @input="name = $event.target.value"
            >
            <input type="number" class="form-control" placeholder="Senchi maratoba ko'rilgan?"
                @input="viewers = $event.target.value"
            >

            <button class="btn btn-outline-dark" type="submit"
                @click="addMovie"
            >Qo'shish</button>
        </form>
    </div>
</template>

<script>
export default{
    data(){
        return {
            name: '',
            viewers: ''
        }
    },

    methods: {
        addMovie(){
            const newMovie = {
                id: Date.now(),
                name: this.name,
                viewers: this.viewers,
                favourite: false,
                like: false
            }

            this.$emit("createMovie", newMovie)

            this.name = ''
            this.viewers = ''
        }
    }
}
</script>