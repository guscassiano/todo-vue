<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue'
  import Formulario from './components/Formulario.vue';
  import Lista from './components/Lista.vue'

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SAAS',
        finalizada: false,
      },
      {
        titulo: 'Ir para academia',
        finalizada: true,
      },
    ]
  })

  const getTarefasPendentes = ()=> {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = ()=> {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = ()=> {
    const { filtro } = estado
    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes()
      case 'finalizadas':
        return getTarefasFinalizadas()
      default:
        return estado.tarefas
    }
  }

  const cadastraTarefa = ()=> {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = ''
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocarFiltro="(e)=> estado.filtro = e.target.value" :tarefa-temp ="estado.tarefaTemp" :editaTarefaTemp="(e)=> estado.tarefaTemp = e.target.value" :cadastraTarefa="cadastraTarefa"/>
    <Lista :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


