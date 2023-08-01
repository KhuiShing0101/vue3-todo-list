<template>
  <div class="App" id="App">
    <h1 class="text-center bg-primary text-white p-3">
      {{ title }}'s Todo Lists
    </h1>
    <div class="container">
      <div class="row py-3">

        <div class="col">
          <input type="text" class="form-control" v-model="newTask" @keyup.enter="addNew()"/>
        </div>

        <div class="col ">
          <button class="btn btn-primary m-1" @click="addNew">
            Add New
          </button>

          <button class="btn btn-warning m-2" @click="deleteTask">
            Delete Task
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

    <div class="col">
      <div class="bg-danger text-white p-3 mt-3 d-flex align-items-center">
        <label class="form-check-label m-0" for="flexSwitchCheckDefault" style="flex: 1; text-align: center; font-size: large;">hide completed tasks</label>
        <div class="form-check form-switch">
          <input class="form-check-input" type="checkbox" id="flexSwitchCheckDefault" v-model="hideCompleteTask">
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
        return this.hideCompleteTask ? this.tasks.filter(v => !v.done): this.tasks;
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

       this.store();
       this.newTask =''
      },

      deleteTask(){
        this.tasks = this.tasks.filter((val)=>!val.done);
        this.store();
      },
      store(){
        localStorage.setItem("myLocalStorage",JSON.stringify(this.tasks))
      }
    },
    mounted(){
      let data = localStorage.getItem("myLocalStorage")
      if(data !== null){
        this.tasks = JSON.parse(data);
      }
    }

  }
</script>

<style>
.line-text{
  text-decoration: line-through;
}
</style>