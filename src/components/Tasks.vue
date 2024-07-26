<template>
    <div>
       <h1 class="display-4 text-center">
         task list
       </h1>
       <hr>
       <div class="row">
         <div class="col-lg-8 offset-lg-2">
            <div class="card mt-4">
                <div class="card-body">
                    <div class="input-group">
                        <input 
                        type="text" 
                        v-model="task"
                        class="form-control form-control-lg"
                        placeholder="add task"
                        >
                        <div class="input-group-append">
                            <button 
                            v-on:click="addTasks()"
                            class="btn btn-success btn-lg"
                            >
                                add
                            </button>
                        </div>
                    </div>
                    <br>
                    <h5
                    v-if="listTasks == 0"
                    >
                    dont tasks for doing
                </h5>
                    <ul class="list-group">
                        <li 
                        v-for="(task, index) in listTasks" :key="index"
                        class="list-group-item d-flex justify-content-between"
                        >
                          <span 
                          class="cursor"
                          v-bind:class="{'text-success' : task.state}"
                          v-on:click="putTasks(task, index)"
                          >
                            <i 
                            v-bind:class="[task.state ? 'fa-solid fa-circle-check'
                                : 'fa-regular fa-circle'
                            ]"
                            >
                        </i>
                          </span>
                          {{ task.name }}
                          <span 
                          class="text-danger cursor"
                          v-on:click="deleteTasks(index)"
                          >
                            <i class="fa-sharp fa-regular fa-trash"></i>
                          </span>
                        </li>
                    </ul>
                </div>
            </div>
         </div>
       </div>
    </div>
</template>

<script>
    export default {
      name: 'Task',
      data() {
        return {
            task: '',
            listTasks: []
        }
      },
      methods: {
        addTasks() {
            const task = {
                name: this.task,
                state: false
            }
            this.listTasks.push(task)
            this.task = ''
        },
        deleteTasks(index) {
            this.listTasks.splice(index, 1)
        },
        putTasks(task, index) {
            this.listTasks[index].state = !task.state
        }
      }
    }
</script>

<style scoped>
 .cursor {
    cursor: pointer;
 }
</style>