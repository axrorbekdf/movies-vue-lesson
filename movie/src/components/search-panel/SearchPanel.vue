<template>
    <div>
        <Input placeholder="Kinolarni qidirish"
            v-model="term"
            @input="changeTermHandler"
        />
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
        changeTermHandler(){
            this.updateTermHandler(this.term)
        }
    }
}
</script>

<style scoped>


</style>