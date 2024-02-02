<script setup>
    const props = defineProps(['tarefas'])
</script>

<template>
    <ul v-if="tarefas != 0" class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in props.tarefas">
        <input @change="e=> tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada === true}" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
    <h4 v-else>Não há tarefas pendentes</h4>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
  h4 {
    margin: 12px;
  }
</style>