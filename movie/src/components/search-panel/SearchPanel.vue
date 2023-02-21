<template>
    <div>
        <input type="text" class="form-control" name="" placeholder="Kinolarni qidirish"
            v-model="term"
            @input="changeTermHandler"
        >
    </div>
</template>

<script>
export default{
    props:{
        updateTermHandler:{
            type: Function,
            required: true
        }
    },
    data(){
        return {
            term: ''
        }
    },
    methods: {
        changeTermHandler(e){
            this.term = e.target.value
            this.updateTermHandler(this.term);
        }
    }
}
</script>

<style scoped>


</style>