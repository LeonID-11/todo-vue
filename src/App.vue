<template>
  <div id="app">
    <input type="text" @keyup.enter="addTask" v-model="currentTask">
    <ul >
      <li 
        v-for="task in tasks" 
        :key="task.id"
        :class="{'strike':task.complited}"
      >
        <input 
          type="text" 
          v-model="task.text"
          v-if="task.isEdit"
        >
        <span
          v-if="!task.isEdit"
          @click="task.complited = !task.complited"
        >{{task.text}}</span>

        <button @click="removeTask(task.id)"> &times; </button>

        <button 
          @click="editTask(task.id)"
          v-html="task.markerBtn"
        ></button>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  },
  data: () => {
    return {
      currentTask: '',
      tasks: [
        { 
          text: 'Изучить JavaScript',
          complited: true,
          id: 2,
          isEdit: false,
          markerBtn: '&#9998;',

        },
        { 
          text: 'Изучить Vue',
          complited: true,
          id: 3,
          isEdit: false,
          markerBtn: '&#9998;',
        },
        { 
          text: 'Создать что-нибудь классное',
          complited: false,
          id: 4,
          isEdit: false,
          markerBtn: '&#9998;',
        }
      ],
    }
  },
  methods:{
    addTask: function() {
      this.tasks.push({
        text: this.currentTask,
        complited: false,
        id: +new Date,
      })
      this.currentTask = ''

    },
    removeTask: function (id){
      console.log(id)
      this.tasks = this.tasks.filter((el)=>{
        return el.id !== id
      })
    },
    editTask: function(id){
      this.tasks = this.tasks.map((task)=>{
        if(task.id === id){
          task.isEdit = !task.isEdit
        if(task.isEdit){
          task.markerBtn = '&#10004;'
        }else{
          task.markerBtn = '&#9998;'
        }
        }
        return task
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}
.strike{
  text-decoration: line-through;
}
</style>
