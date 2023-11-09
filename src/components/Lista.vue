<script setup>
  const props = defineProps(['tarefas'])
</script>


<template>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input
        required
        @change="(e) => (tarefa.finlizada = e.target.checked)"
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
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
