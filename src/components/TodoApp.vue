<template>
  <div class="container">
    <h2 class="text-center mt-5">Vue Todo</h2>

    <!-- Input -->
    <div class="d-flex mt-5">
      <input v-model="task" type ="text" placeholder="Enter Task" class="form-control">
      <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>
  
  <!-- Tabela de tarefas -->
  <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key = "index">
      <td>
        <span :class="{'finished':task.status === 'finished'}">{{task.name}}</span>
        </td>
      <td style="width: 120px">
        <span @click="changeStatus(index)" class ="pointer"
        :class="{'text-danger': task.status === 'to-do',
        'text-success': task.status === 'finished'
        }"
        >
        {{task.status}}
        </span>
        </td>
      <td>
          <div class="text-center pointer" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
          <div class="text-center pointer" @click="deleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
  </tbody>
  </table>

  <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(finishedTask,index) in finishedTasks" :key = "index">
      <td>
        <span :class="{'finished':finishedTask.status === 'finished'}">{{finishedTask.name}}</span>
        </td>
      <td style="width: 120px">
        <span @click="changeStatustodo(index)" class ="pointer"
        :class="{'text-danger': finishedTask.status === 'to-do',
        'text-success': finishedTask.status === 'finished'
        }"
        >
        {{finishedTask.status}}
        </span>
        </td>
      <td>
          <div class="text-center pointer" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
          <div class="text-center pointer" @click="deleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
  </tbody>
  </table>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      task: ``,
      editedTask: null,
      availableStatus: ['to-do', 'finished'],

      tasks: [
      {
        name: 'Learn Vue.',
        status: 'to-do'
      },
            {
        name: 'Learn Laravel.',
        status: 'to-do'
      }
      ],

      finishedTasks:[]
    }
  },

  methods: {
    submitTask(){
      if(this.task.length === 0) return;

      if(this.editedTask ===null){

      this.tasks.push({
        name: this.task,
        status: 'to-do'
      });
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      this.task = '';
  },

  deleteTask(index){
    this.tasks.splice(index,1);
  },

  editTask(index){
    this.task = this.tasks[index].name;
    this.editedTask = index;

  },

  changeStatus(index){
    let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
    if(++newIndex >1) newIndex = 0;
    
    this.tasks[index].status = this.availableStatus[newIndex];
    this.finishedTasks.push(this.tasks[index])
    
    this.tasks.splice(index, 1)
  },

  changeStatustodo(index){
    this.finishedTasks[index].status = 'to-do'
    this.tasks.push(this.finishedTasks[index])

    this.finishedTasks.splice(index, 1)
  }

  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.pointer{
  cursor: pointer;
}

.finished{
  text-decoration: line-through;

}
</style>
