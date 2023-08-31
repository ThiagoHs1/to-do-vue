<script setup>
import { reactive } from 'vue'
import cabecalho from './components/cabecalho.vue'
import formulario from './components/formulario.vue'
import listadetarefas from './components/listadetarefas.vue'

  const estado = reactive({
    filtro: 'Todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar React',
        finalizado: false,
      },
      {
        titulo: 'Estudar Vue',
        finalizado: false,
      },
      
      {
        titulo: 'Estudar Sass',
        finalizado: true,
      }
      

    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizado === false)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizado)
  }

  const getTarefasFiltradas = () => {
   const {filtro} = estado;

      switch (filtro) {
        case 'Pendentes':
          return getTarefasPendentes();
        case 'Finalizadas':
          return getTarefasFinalizadas();
        default:
          return estado.tarefas;
      }
    }

  
      const cadastrarTarefa = (titulo) => {
      
      const novaTarefa = {
        titulo: estado.tarefaTemp,
        finalizado: false
      }
      estado.tarefas.push(novaTarefa);
      estado.tarefaTemp = '';
      }
</script>

<template>
  <div class="container">
    <cabecalho :tarefas-pendentes="getTarefasPendentes().length" />

    <formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :cadastrar-tarefa="cadastraTarefa" :edita-tarefa-temp=" evento => estado.tarefaTemp = evento.target.value" />
    <listadetarefas :tarefas="getTarefasFiltradas()"/> 


  

  </div>


</template>

