<template>
  <div class="todo-list">
    <h1>Lista de Tarefas</h1>

    <div class="add-task">
      <input type="text" placeholder="Adicionar nova tarefa" v-model="newTask">
      <Button @click="addTask">Adicionar</Button> 
    </div>

    <div v-if="tasks.length > 0" class="tasks">
      <div v-for="(task, index) in tasks" :key="index" class="task align-items-center gap-3 mb-4">
        <span>{{ task }}</span>
        <Button @click="removeTask(index)" icon="pi pi-times" severity="danger" text rounded aria-label="Cancel"/>
      </div>
    </div>
    <div v-else>
      <p>Nenhuma tarefa adicionada ainda.</p>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import Button from 'primevue/button'; 

const newTask = ref('');
const tasks = ref([]);

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = ''; 
  }
};

const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

export default {
  name: 'ToDoItem',
  components: { 
    Button
  },
  setup() {
    return {
      newTask,
      tasks,
      addTask,
      removeTask
    };
  }
};

</script>

<style>
.todo-list {
  max-width: 400px;
  margin: auto;
  text-align: center;
}

.add-task input {
  padding: 5px;
  margin-right: 10px;
}

.add-task button {
  padding: 5px 10px;
}

.task {
  margin-top: 10px;
}

.tasks {
  margin-top: 20px;
}

.task span {
  line-height: 2.5; 
}
</style>
