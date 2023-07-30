<template>
  <div class="">
    <h1 class="text-center bg-primary text-white p-3">
      {{ title }}'sTodo Lists
    </h1>
    <div class="container">

      <div class="row">
        <div class="col fs-3 mb-4">Tasks</div>
        <div class="col-2 fs-3 mb-4">Done</div>
      </div>

      <div class="row" v-for="(task, key) in tasks" :key="key">

        <div class="col" 
          :class="task.done ? 'line-text' : ''">{{ task.action }}</div>

        <div class="col-2">
          <input type="checkbox" v-model="task.done">
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
      tasks:[
        {action: "buy new phone", done:false},
        {action: "buy new shoe",  done:true},
        {action: "Call Aung Aung", done:false},
        {action: "buy new shirt", done:false},
      ]
    })
  }
</script>

<style>
.line-text{
  text-decoration: line-through;
}
</style>
