<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import Tarefas from './components/Tarefas.vue';

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
      },
    ]
  });
  
const getTarefasPendentes = () => {
return estado.tarefas.filter(tarefa => !tarefa.finalizada );
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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <Tarefas :tarefas="getTarefasFiltradas()" :quantidade-de-tarefas="getTarefasFiltradas().length" />
  </div>

  
  
</template>

<style scoped>

</style>
