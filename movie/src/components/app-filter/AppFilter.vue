<template>
    <div>
        <div class="btn-group mt-2">

            <button class="btn" 
                v-for="button in filterButtons" :key="button.name"
                @click="filterHandler(button.name)"
                :class = "[filterName == button.name ? 'btn-dark':'btn-outline-dark']"
            > {{ button.title }}</button>
        </div>
    </div>
</template>

<script>
    export default{
        props:{
            updateFilterHandler:{
                type: Function,
                required: true
            },
            filterName:{
                type: String,
                required: true
            }
        },
        data(){
            return {
                filterButtons: [
                    {
                        title: "Barcha kinolar",
                        name: 'all'
                    },
                    {
                        title: "Mashxur kinolar",
                        name: 'popular'
                    },
                    {
                        title: "Eng ko'p ko'rilgan kinolarr",
                        name: 'mostViewers'
                    },
                ],
                filter: 'all'
            }
        },
        methods:{
            filterHandler(filter){
                this.filter = filter
                this.updateFilterHandler(this.filter)
            }
        }
    }
</script>