<template>
    <div class="pt-3">
        <h1 class="h3">Yangi kino qo'shish</h1>
        <form action="" class="d-flex" @submit.prevent>
            <input type="text" class="form-control" placeholder="Qanday kino?"
                v-model="name"
            >
            <input type="number" class="form-control" placeholder="Senchi maratoba ko'rilgan?"
                v-model="viewers"
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
            
            if(!this.name || !this.viewers) return false;

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