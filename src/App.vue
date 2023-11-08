<script setup>
import { reactive } from 'vue';

const estado = reactive({
  tarefaValue: '',
  filtro: "todas",
  tarefas:[
    {
      titulo:'Estudar Es6',
      finlizada:true
    },
    {
      titulo:'Estudar SASS',
      finlizada:false
    },
    {
      titulo:'Academia',
      finlizada:false
    }

  ]
})

const gettTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finlizada)
}

const gettTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finlizada)
}

const gettTarefasFiltradas = () => {
  const { filtro } = estado

  switch (filtro) {

    case "pendentes":
      return gettTarefasPendentes()
    case "finalizadas":
      return gettTarefasFinalizadas()
    default:
      return estado.tarefas
  }

}

const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaValue,
      finalizada: false
    }

    estado.tarefas.push(tarefaNova)
    estado.tarefaValue = ""
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light">
      <h1>Minhas Tarefas</h1>
      <p>Voce possui {{ gettTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastraTarefa()">
      <div class="row">
        <div class="col">
          <input
            required
            :value="estado.tarefaValue"
            @change=" e => estado.tarefaValue = e.target.value"
            type="text"
            placeholder="Digite o título da Tarefa"
            class="form-control"
          />
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Enviar</button>
        </div>
        <div class="col-md-2">
          <select
            @change="(evento) => (estado.filtro = evento.target.value)"
            class="form-control"
          >
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form >
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in gettTarefasFiltradas()">
        <input 
          required
          @change="e => tarefa.finlizada = e.target.checked"
          :checked="tarefa.finlizada"
          :id="tarefa.titulo"
          type="checkbox"
        />
        <label
          v-bind:class="{ done: tarefa.finlizada }"
          class="ms-3"
          :for="tarefa.titulo"
          >{{ tarefa.titulo }}</label
        >
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
