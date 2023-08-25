<script setup>
//const props = defineProps(['title','content','id']);
const props = defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: 'Sin contenido'
    }
})

const emit = defineEmits(['setFavorite'])

</script>

<template>
    <div :id="props.id" class="card">
        <div class="card-body">
            <h5 class="card-title">{{props.id}}.- {{ props.title }}</h5>
            <p>{{ props.body }}</p>
            <button @click="emit('setFavorite', props.title)" class="btn btn-warning"><i class="fa-solid fa-star"></i></button>
        </div>
    </div>
</template>
