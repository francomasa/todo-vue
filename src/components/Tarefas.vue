
<script setup>
    const props = defineProps(['tarefas', 'quantidadeDeTarefas']);
</script>


<template>
    <ul v-if="props.quantidadeDeTarefas" class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
        </li>
    </ul>
    <h3 class="mt-4 ms-2" v-else>Não tem tarefas</h3>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>