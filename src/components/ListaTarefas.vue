<script setup>
    const props = defineProps(['tarefas', 'tarefasPendentes'])

</script>

<template>
    <ul v-if="!props.tarefasPendentes " class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
        <input
            @change="(evento) => (tarefa.finalizada = evento.target.checked)"
            :checked="tarefa.finalizada"
            :id="tarefa.titulo"
            type="checkbox"
        />
        <label
            :class="{ done: tarefa.finalizada }"
            class="ms-3"
            :for="tarefa.titulo"
        >
            {{ tarefa.titulo }}
        </label>
        </li>
    </ul>
    <h2 v-else class="m-5">Sem tarefas pendentes</h2>
</template>

<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>