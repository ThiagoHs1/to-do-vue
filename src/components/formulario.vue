<script setup>
    const props = defineProps(['cadastrarTarefa', 'TarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
<form @submit.prevent="props.cadastrarTarefa" >
    <div class="row">
        <div class="col">
            <input required :value="props.tarefaTemp" @change="props.editaTarefaTemp" type="text" placeholder="Digite sua tarefa" class="form-control" name="" id="">
        </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select   @change ="props.trocarFiltro" name="" class="form-control" >
                    <option value="Todas">Todas tarefas</option>
                    <option value="Pendentes">Tarefas pendentes</option>
                    <option value="Finalizadas">Tarefas finalizadas</option>
                </select>
            </div>
        </div>
</form>
</template>