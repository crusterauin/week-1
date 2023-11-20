<script setup>
import { ref, computed } from 'vue';

const tasks = ref([]);

const taskInput = ref('');
const dueDateInput = ref('');

const addTask = () => {
  if (taskInput.value && dueDateInput.value) {
    tasks.value.push({
      id: tasks.value.length + 1,
      name: taskInput.value,
      due: dueDateInput.value,
      status: 'On Process'
    });

    taskInput.value = '';
    dueDateInput.value = '';
  }
};

const completeTask = (taskId) => {
  const taskIndex = tasks.value.findIndex(task => task.id === taskId);
  if (taskIndex !== -1) {
    tasks.value[taskIndex].status = 'Completed';

    setTimeout(() => {
      tasks.value.splice(taskIndex, 1);
    }, 3000);
  }
};

const isDuePast = (dueDate) => {
  const today = new Date();
  const due = new Date(dueDate);

  return due < today;
};

const hasTasks = computed(() => tasks.value.length > 0);
</script>



<style>
  body {
    background: linear-gradient(180deg, #232D3F 0%, #000 100%);
    display: flex;
    justify-content: center;
  }

  .header>h1 {
    font-family: Plus Jakarta Sans;
    font-size: 8rem;
    font-style: normal;
    font-weight: 700;
    line-height: normal;
    background: linear-gradient(90deg, #008170 0%, #005B41 100%);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    text-align: center;
    margin-bottom: 0;
  }

  .header>p {
    color: #FFF;
    font-family: Plus Jakarta Sans;
    font-size: 1.5rem;
    font-style: normal;
    font-weight: 700;
    line-height: normal;
    text-align: center;
    margin-top: 0;
  }

  .header>p>span {
    color: #FFF;
    font-family: Plus Jakarta Sans;
    font-size: 1.5rem;
    font-style: normal;
    font-weight: 500;
    line-height: normal;
  }

  .input {
    display: flex;
    justify-content: center;
    margin-top: 3rem;
    margin-bottom: 1rem;
    margin-top: 5rem;
  }

  .input>form {
    display: flex;
    align-items: center;
    column-gap: 1rem;
  }

  .addTask > input[type=text] {
    width: 60rem !important;
    height: 3.625rem !important;
    flex-shrink: 0 !important;
    border-radius: 0.625rem !important;
    background: #D9D9D9 !important;
    color: #232D3F !important;
    font-family: 'Plus Jakarta Sans' !important;
    font-size: 2rem !important;
    font-style: normal !important;
    font-weight: 500 !important;
    line-height: normal !important;
    opacity: 0.5 !important;
    border-radius: 0.625rem !important;
    background: #D9D9D9 !important;
    z-index: 1!important;
  }

  ::placeholder {
    padding-left: 1rem;
  }

  .addTask >input[type=date] {
    width: auto;
    height: 2.875rem;
    flex-shrink: 0;
    border-radius: 0.625rem;
    background: #008170;
    z-index: 2;
    color: #D9D9D9;
    color: #D9D9D9;
    font-family: Plus Jakarta Sans;
    font-size: 2rem;
    font-style: normal;
    font-weight: 500;
    line-height: normal;
    position: absolute;
    margin-left: 41.8rem;
  }

  .addTask >input[type=submit] {
    width: 9.0625rem;
    height: 3.625rem;
    flex-shrink: 0;
    border-radius: 0.625rem;
    background: #008170;
    font-family: Plus Jakarta Sans !important ;
    color: #D9D9D9 !important;
    font-size: 2rem !important;
    font-style: normal !important;
    font-weight: 700 !important;
    line-height: normal !important;
    z-index: 0;
  }

  .borderTabel {
    display: flex;
    justify-content: center;
    background-color: #005B41;;
    padding: 1rem;
    border-radius: 1rem;
    margin-bottom: 14.5rem;
  }

  th {
    font-weight: 700 !important;
  }

  .tabel, table, th, td{
    border: 0.2rem solid;
    background-color: transparent;
    border-color: white;
    font-family: 'Plus Jakarta Sans';
    font-size: 2rem;
    font-style: normal;
    font-weight: 500;
    line-height: normal;
    padding: 0.5rem;
    border-collapse: collapse;
    border-radius: 1rem; 
  }

  .tabel td.due-past {
    color: red;
  }

  .tabel button {
    border-radius: 0.625rem;
    background: #008170;
    color: #D9D9D9;
    font-family: 'Plus Jakarta Sans';
    font-size: 1rem;
    font-style: normal;
    font-weight: 700;
    line-height: normal;
  }

  .task {
    padding-right: 20rem;
  }

  .due{
    padding-right: 14rem;
  }

  .status {
    padding-right: 7rem;
  }

  .noTasks {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    color: #FFF;
    margin-top: 2rem;
    margin-bottom: 19.8rem;
  }
</style>

<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:ital,wght@0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,200;1,300;1,400;1,500;1,600;1,700;1,800&display=swap" rel="stylesheet">
  <body>
    <div class="main">
      <div class="header">
        <h1>To Do Today</h1>
        <p>By <span>Faturrohman Fairuz Zaki</span></p>
      </div>
      <div class="input">
        <form @submit.prevent="addTask" class="addTask">
          <input v-model="taskInput" type="text" id="task" name="task" placeholder="Add Your Task Here">
          <input v-model="dueDateInput" type="date" name="dueDate" placeholder="Due">
          <input type="submit" value="Submit">
        </form>
      </div>
      <div v-if="hasTasks" class="borderTabel">
        <table class="tabel">
          <tr>
            <th class="no">No</th>
            <th class="task">Task</th>
            <th class="due">Due</th>
            <th class="status">Status</th>
            <th class="action">Action</th>
          </tr>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ task.name }}</td>
            <td :class="{ 'due-past': isDuePast(task.due) }">{{ task.due }}</td>
            <td>{{ task.status }}</td>
            <td>
              <button v-if="task.status === 'On Process'" @click="completeTask(task.id)">Complete</button>
              <button v-else disabled>Completed</button>
            </td>
          </tr>
        </table>
      </div>
      <div v-else class="noTasks">
        Yay, no tasks today!
      </div>
    </div>
  </body>
</template>
