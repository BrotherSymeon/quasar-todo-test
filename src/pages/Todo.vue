<template>
  <q-page class="bg-grey-4 column">
    <div class="row q-pa-sm bg-primary">
    <q-input filled
    @keyup.enter="addTask"
    class="col"
    square
    bg-color="white"
    v-model="newTask" 
    placeholder="What Now?" dense>


        <template v-slot:append>
          <q-btn
            @click.stop="addTask"
          round dense flat icon="add" />
        </template>
      </q-input>
    </div>
  <q-list 
    class="bg-white"
    seperator
    bordered
  >
      <q-item
      v-for="(task, index) in tasks" 
      @click="task.done = !task.done"
      clickable
      :class="{'done bg-blue-1': task.done}"
      v-bind:key="index"
      v-ripple>
        <q-item-section avatar>
          <q-checkbox 
          class="no-pointer-events"
          v-model="task.done" 
          color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
         <q-item-section
         v-if="task.done"
         side>
         <q-btn 
            @click.stop="deleteTask(index)"
            outline 
            round 
            dense 
            color="primary" icon="delete" /> 
        </q-item-section>
      </q-item>

    </q-list>
  <div 
    v-if="!tasks.length"
    class="no-tasks absolute-center">
  <q-icon 
    name="check"
    size="100px"
    color="primary"/>
    <div class="text-h5 text-primary text-center">
      Done!
    </div>
  </div>
  </q-page>
</template>

<script>

import { Dialog } from 'quasar';

export default {
  data(){
    return{
      newTask: '',
      tasks:[
        //{title: 'Go To the  Monastery', done: false},
        //{title: 'Get Humble', done: false},
        //{title: 'Find Salvation', done: false}
      ]
    }
  },
  methods: {
    deleteTask(index){
      this.$q.dialog({
        title: 'Confirm',
        message: 'Are you sure you want to delete this task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1);
        this.$q.notify({
          message: 'Task Down! Great Job!',
          color: 'dark'
        })
      })
    },
    addTask(){
      
      if(this.newTask.length){
        this.tasks.push({
          title: this.newTask,
          done: false
        });
        this.newTask = '';
      }
    }
  }
}
</script>
<style lang="scss">
.done{
.q-item__label{
  text-decoration:line-through;
  color: #bbb
}
}
.no-tasks{
  opacity: 0.5
};
</style>
