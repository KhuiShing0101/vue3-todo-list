<template>
  <div class="App">
    <h1 class="text-center bg-primary text-white p-3">
      {{ title }}'sTodo Lists
    </h1>
    <div class="container">
      <div class="row py-3">

        <div class="col">
          <input type="text" class="form-control" v-model="newTask" @keyup.enter="addNew()"/>
        </div>

        <div class="col">
          <button @click="addNew">
            Add New
          </button>
        </div>

      </div>
      <div class="row">
        <div class="col fs-3 mb-4" >Tasks</div>
        <div class="col-2 fs-3 mb-4" >Done</div>
      </div>

      <div v-if="filterTask.length > 0">
        <div class="row" v-for="(task, key) in filterTask" :key="key">
          <div class="col" 
            :class="task.done ? 'line-text' : ''">{{ task.action }}
          </div>
          <div class="col-2">
            <input type="checkbox" v-model="task.done">
          </div>
        </div>
      </div>
      
      <div class="alert alert-warning text-center mb-3 mt-3" 
      v-else >There is no data</div>

      <div col="row">
        <div class="bg-danger text-center text-white p-3 row mt-3">
          <div class="form-check form-switch">
            <input class="form-check-input" type="checkbox" id="flexSwitchCheckDefault" v-model="hideCompleteTask">
            <label class="form-check-label" for="flexSwitchCheckDefault">hide completed tasks</label>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
  export default{
    name: "App",
    data: () => ({
      title:'HKS',
      newTask:'',
      hideCompleteTask:false,
      tasks:[
      ],
    }),
    computed:{
      filterTask() {
        return this.hideCompleteTask ? this.tasks.filter(v => !v.done):
        this.tasks;
      }
    },
    methods: {
      addNew(){
        if(this.newTask === ''){
          return  alert("Please fill new task")
        }
       this.tasks.push({
        action:this.newTask,
        done:false,
       }),
       this.newTask =''
      }
    },
  }
</script>

<style>
.line-text{
  text-decoration: line-through;
}
</style>