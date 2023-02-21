<template>
    <Box>
        <h1 class="h3">Yangi kino qo'shish</h1>
        <form action="" class="d-flex" @submit.prevent>
            <Input placeholder="Qanday kino?"
                v-model="name"
            />
            <Input type="number" placeholder="Senchi maratoba ko'rilgan?"
                v-model="viewers"
            />

            <PrimaryButton class="btn-outline-dark" type="submit"
                @click="addMovie"
            >Qo'shish</PrimaryButton>
        </form>
    </Box>
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