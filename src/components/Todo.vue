<template>
    <div class="container" >
        <h2 class="text-center mt-5" >Todo List</h2>
        <div class="d-flex">
            <input v-model="task" type="text" placeholder="Tarefa:" class="form-control">
            <button @click="submitTask" class="btn btn-warning roudend-0">Adicionar</button>
        </div>
<table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Tarefa</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center" >#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(tasks, index) in tasks" :key="index">
      <td><span :class="{'finished': tasks.status === 'Terminada'}" >{{tasks.name}}</span></td>
      <td style="width: 120px" > <span  @click="changeStatus(index)" class="pointer" :class="{'text-danger': tasks.status === 'Pendente','text-success': tasks.status === 'Terminada', 'text-warning': tasks.status === 'Em Progresso'  }" >{{tasks.status}}</span></td>
        <td>
            <div @click="editTask(index)" class="text-center"  >
                <span class="fa fa-pen"></span>
            </div>
        </td>
        <td>
            <div @click="deleteTask(index)" class="text-center" >
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
    data() {
        return {
            task: '',
            editedTask: null,
            availableStatus: ['Pendente',  'Em Progresso', 'Terminada'],
            tasks: [
                
            ]
        }
    },
    methods: {
        submitTask(){
            if(this.task.length === 0) return;

            if(this.editedTask === null){
                this.tasks.push({
                    name: this.task,
                    status: 'to do'
                });
            }else{
                this.tasks[this.editedTask].name = this.task
                this.editedTask = null
            }
                this.task = ''
            },

        deleteTask(index){
            this.tasks.splice(index, 1)
        },

        editTask(index){
            this.task = this.tasks[index].name
            this.editedTask = index
        },
        changeStatus(index){
            let newIndex = this.availableStatus.indexOf(this.tasks[index].status)
            if(++newIndex > 2) newIndex = 0
            this.tasks[index].status = this.availableStatus[newIndex]
        }
    }
}
</script>

<style>
.pointer{
    cursor: pointer;
}
.finished{
    text-decoration: line-through;
    background-color: rgb(51, 247, 51);
}
</style>