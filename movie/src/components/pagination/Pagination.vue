<template>
    <nav aria-label="pagination" class="d-flex justify-content-end mt-2">
        <ul class="pagination pagination-md">
            <li 
                v-for="pageNumber in pageCount" 
                :key="pageNumber" 
                class="page-item" 
                :class="{active: pageNumber == activePage}" 
                aria-current="page"
                @click="changePage(pageNumber)"
                style="cursor: pointer;"
            >
                <span class="page-link"> {{ pageNumber }}</span>
            </li>
        </ul>
    </nav>
</template>

<script>
export default{
    props:{
        activePage:{
            type: Number,
            required: true
        },
        pageCount: {
            type: Number,
            required: true
        },
        changePage:{
            type: Function,
            required: true
        }
    },
}
</script>