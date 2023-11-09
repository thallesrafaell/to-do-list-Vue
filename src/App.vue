<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/cabecalho.vue'
  import Formulario from './components/formulario.vue'
  import Lista from './components/lista.vue'
  


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
    <Cabecalho :tarefas-pendentes="gettTarefasPendentes().length"/>
    <Formulario :tarefa-value="estado.tarefaValue" :edita-tarefa="e => estado.tarefaValue = e.target.value" :cadastrar-tarefa="cadastraTarefa" :trocar-filtro="e => estado.filtro = e.target.value"/>
    <Lista :tarefas="gettTarefasFiltradas()"/>

  </div>
</template>


