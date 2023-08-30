<script setup>
import { reactive } from 'vue'
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
  <div class="contain">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1> Minhas Tarefas </h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas a serem feitas.</p>
    </header>
  <form @submit.prevent="cadastrarTarefa" >
    <div class="row">
      <div class="col">
        <input required :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" type="text" placeholder="Digite sua tarefa" class="form-control" name="" id="">
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select   v-model="estado.filtro" name="" class="form-control" >
          <option value="Todas">Todas tarefas</option>
          <option value="Pendentes">Tarefas pendentes</option>
          <option value="Finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>

  <ul class="list-group mt-4">
    <li class="list-group-item " v-for="tarefa in getTarefasFiltradas()" >
      <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" id="tarefa.titulo" type="checkbox" >
      <label class = "form-check-label ms-3" :class="{done: tarefa.finalizado}" :for="tarefa.titulo">{{tarefa.titulo}}</label>
    </li>
  </ul>

  </div>


</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
