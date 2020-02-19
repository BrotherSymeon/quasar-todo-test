<template>
  <q-page class="bg-grey-4 column">
  <q-list 
    class="bg-white"
    seperator
    bordered
  >
      <q-item
      v-for="task in tasks" 
      @click="task.done = !task.done"
      clickable
      :class="{'done bg-blue-1': task.done}"
      key="task.title"
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
          x
        </q-item-section>
      </q-item>

    </q-list>

  </q-page>
</template>

<script>
export default {
  data(){
    return{
      tasks:[
        {title: 'Go To the  Monastery', done: false},
        {title: 'Get Humble', done: false},
        {title: 'Find Salvation', done: false}
      ]
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

</style>