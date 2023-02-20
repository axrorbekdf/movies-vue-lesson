<template>
    <div class="container">
        <h1>Counter: {{ counter }}</h1>
        <button @click="add" class="btn btn-success">Add</button>
        <button @click="deletes" class="btn btn-danger">Delete</button>
    </div>
</template>

<script>

export default {
    data(){
        return {
            counter: 0
        }
    },
    methods: {
        add(){
            this.counter += 1
        },

        deletes(){
            if(this.counter == 0)
                return false
            
            this.counter -= 1
        }
    }
}

</script>

<style>

</style>