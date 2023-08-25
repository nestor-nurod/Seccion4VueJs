<script setup>
    const emit = defineEmits(['nextPage','previousPage']);

    const props = defineProps(['start','end','posts']);
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button :disabled="start<=0" @click="emit('previousPage')" type="button" class="btn btn-outline-primary">Atras</button>
        <button :disabled="end>=posts" @click="emit('nextPage')" type="button" class="btn btn-outline-primary">Siguiente</button>
    </div>
</template>