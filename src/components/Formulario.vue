
<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp']);
</script>

<template>
    <!-- 
    para fazer o submit do formulario sem atualizar
    o site, usamos o .prevent
       -->
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required
                    type="text" class="form-control" placeholder="Digite aqui a descripção da tarefa" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="from-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Tarefas Pendentes</option>
                    <option value="finalizadas">Tarefas Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>