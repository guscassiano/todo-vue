<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaTarefas from './components/ListaTarefas.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemporaria: '',
    tarefas: [{
      titulo: 'Estudar ES6',
      finalizada: false
    },
    {
      titulo: 'Estudar React',
      finalizada: false
    },
    {
      titulo: 'Ir à academia',
      finalizada: true
    }]
  })

  const getTarefasPendentes = ()=> {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = ()=> {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = ()=> {
    const {filtro} = estado

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
      titulo: estado.tarefaTemporaria,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemporaria = ''
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temporaria="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaTarefas :tarefas="getTarefasFiltradas()" :tarefas-pendentes="getTarefasPendentes()"/>
  </div>
</template>

