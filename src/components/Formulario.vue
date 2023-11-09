<script setup>
const props = defineProps(['cadastrarTarefa', 'tarefaValue', 'trocarFiltro', 'editaTarefa'])
</script>

<template>
  <form @submit.prevent="props.cadastrarTarefa">
    <div class="row">
      <div class="col">
        <input
          required
          :value="props.tarefaValue"
          @change="props.editaTarefa"
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
          @change="props.trocarFiltro"
          class="form-control"
        >
          <option value="todas">Todas Tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>