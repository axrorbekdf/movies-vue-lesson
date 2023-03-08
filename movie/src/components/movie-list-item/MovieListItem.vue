<template>
    <li class="list-group-item d-flex justify-content-between align-items-center" :class="[{like:movie.like}, {favourite: movie.favourite}]">
        <span 
            class="item-pro" 
            @click="$emit('onToggle', {id: movie.id, prop: 'like'})"
            style="cursor: pointer;"
        >
            {{ movie.name }}
        </span>

        <div style="display: inherit;">
            <input 
                type="text" 
                class="form-control-sm col-2" 
                :value="movie.viewers"
            >

            <div class="btn-group d-flex justify-content-between align-items-center">
                <button class="btn-sm btn-cookie" @click="$emit('onToggle', {id: movie.id, prop: 'favourite'})">
                    <i class="fas fa-cookie"></i>
                </button>
                <button class="btn-sm btn-trash" @click="$emit('onRemove', movie.id)">
                    <i class="fas fa-trash"></i>
                </button>

                <i class="fas fa-star"></i>
            </div>
        </div>
    </li>
</template>

<script>
export default{
    props:{
        movie: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped>
input{
    width: 100px;
}
.btn-cookie{
    color: #c3b10e;
}
.btn-trash{
    color: #dc2039;
}

button{
    margin: 0 5px;
}
button, input{
    border: none;
}

.list-group-item .fa-star{
    color: #ffd700;
    transition: 0.3s all;
    transform: translateX(30px);
    opacity: 0;
}

.list-group-item.like .fa-star{
    transform: translateX(0);
    opacity: 1;
}

.list-group-item.favourite .item-pro, 
.list-group-item.favourite .form-control-sm{
    color: #c3b10e;
}
</style>