<template>  
    <div>
        <h5 class="card-header handle">{{column.title}}</h5>
        <draggable :list="column.tasks" :animation="300" group="tasks">
            <Task
                v-for="(task) in column.tasks"
                :key="task.id"
                :task="task"
                class="card smallcard"
                v-bind:class="{ faved: task.isFaved }"
                :msg = "task"
                >
            </Task>
        </draggable>
        <div v-if="column.editing">
            <input type="text" v-model="newTask.title" placeholder="" class="newinput"/>
            <button type="button" @click="add(column)" class="btn btn-light btn-sm w-50"><b-icon-check2 variant="success"></b-icon-check2></button>
            <button type="button" @click="editing(column)" class="btn btn-light btn-sm w-50" ><b-icon-x-circle-fill variant="danger"></b-icon-x-circle-fill></button>
        </div>
        <button v-else type="button" @click="editing(column)" class="btn btn-light btn-display"><b-icon-plus></b-icon-plus></button>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import draggable from "vuedraggable";
import { BIconStar, BIconPencilSquare, BIconPlus, BIconCheck2, BIconXCircleFill} from 'bootstrap-vue'

import Task from './Task.vue';

Vue.component('BIconXCircleFill', BIconXCircleFill)
Vue.component('BIconCheck2', BIconCheck2)
Vue.component('BIconPlus', BIconPlus)
Vue.component('BIconStar', BIconStar)
Vue.component('BIconPencilSquare', BIconPencilSquare)

@Component({
  components: {
    draggable,
    Task
  }
})

export default class TasksList extends Vue {
  @Prop() private column!: Array<object>;
  
    public newTask: Record<string, any> = {
    id: 0,
    title: "",
    timestamp: "",
    isFaved: false,
    isEdited: false
  }

  public add(column): void {
    const newId = column.tasks.length+1;
    const d = new Date();
    this.newTask.id = newId;
    this.newTask.timestamp = d.getFullYear() + "-" + d.getMonth() + "-" + d.getDay() + " " + d.getHours() + ":" + d.getMinutes() + ":" + d.getSeconds();
    column.tasks.push(this.newTask);    
    column.editing = !column.editing;
    this.newTask = {
      id: 0,
      title: "",
      timestamp: "",
      isFaved: false,
      isEdited: false
    }
  }

    public editing(column): void {
    column.editing = !column.editing;
    this.newTask = {
      id: 0,
      title: "",
      timestamp: "",
      isFaved: false,
      isEdited: false
    }
  }
}
</script>

<style scoped>
.newinput {
  width: calc(100% - 20px);
  position: relative;
  margin: 10px;
  border: 1px solid rgb(194, 194, 194);
  border-radius: 2px;
  display: block;
}
</style>