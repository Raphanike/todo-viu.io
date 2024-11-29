<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import listaDeTarefas from './components/ListaDeTarefas.vue';
  



const estado = reactive({
  filtro:'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar Sass',
      finalizada: false,
    },
    {
      titulo: 'Ir pra academia',
      finalizada: true,
    }
  ]
})

const TarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const TarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro} = estado; 

  switch (filtro) {
    case 'pendentes':
      return TarefasPendentes();
    case 'finalizadas':
      return TarefasFinalizadas();
    default:
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
    <Cabecalho :tarefas-pendentes="TarefasPendentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <listaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
  
</template>


