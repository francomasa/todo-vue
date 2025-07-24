<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: "todas",
    tarefaTemp: '',
    tarefas: [
      {
        titulo: "Estudar ES6",
        finalizada: false,
      },
      {
        titulo: "Estudar SASS",
        finalizada: false,
      },
      {
        titulo: "Ir para academia",
        finalizada: true,
      }
    ]
  });
  
const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}


const getTarefasFiltradas = () => {
  const { filtro } = estado;
  switch(filtro){
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    case 'todas':
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <!-- 
    para fazer o submit do formulario sem atualizar
    o site, usamos o .prevent
       -->
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" class="form-control" placeholder="Digite aqui a descripção da tarefa" />
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="from-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas Pendentes</option>
            <option value="finalizadas">Tarefas Finalizadas</option>
          </select>
        </div>

        <ul class="list-group mt-4">
          <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
          </li>
        </ul>
      </div>
    </form>
  </div>

  
  
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
