<template>  
    <div>
        <h6 class="card-header font-weight-bold handle">{{column.title}}</h6>
        <draggable :list="column.tasks" :animation="300" group="tasks" :move="checkMove">
            <Task
                v-for="(task, i) in filteredTasks()"
                :key="`${i}-${task.id}`"
                class="smallcard card"
                v-bind:class="{ faved: task.isFaved }"
                :task = "task"
                :users = "users"
                >
            </Task>
        </draggable>
          <div class="card-footer text-muted p-0">
            <div v-if="column.editing">
                  <input type="text" v-model="newTask.title" placeholder="" class="newinput"/>
                  <button type="button" @click="add(column)" class="btn btn-sm w-50"><b-icon-check2 variant="success"></b-icon-check2></button>
                  <button type="button" @click="editing(column)" class="btn btn-sm w-50" ><b-icon-x-circle-fill variant="danger"></b-icon-x-circle-fill></button>
            </div>
            <button v-else type="button" @click="editing(column)" class="btn btn-display"><b-icon-plus></b-icon-plus></button>
          </div>
        </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import draggable from "vuedraggable";

import Task from './Task.vue';

@Component({
  components: {
    draggable,
    Task
  }
})
export default class TasksList extends Vue {
  @Prop() private column;
  @Prop() private selected!: number;
  @Prop() private users;

  public checkMove(evt) {
      const projectManagers = [];
      this.users.filter(user => user.job_title == "Project Manager").forEach(element => {
          projectManagers.push(element.id);
      });
    if (evt.relatedContext.component.$parent.column.id == 5) {
      if (projectManagers.includes(evt.draggedContext.element.owner)) {
        return 1;
      } else {
          return false;
      }
    } else return 1;
  }

    public filteredTasks() {
        if (this.selected == 0) {
            return this.column.tasks;
        } else {
            return this.column.tasks.filter(task => task.owner == this.selected);
        }
    }
  
    public newTask = {
        id: 0,
        title: "",
        timestamp: "",
        isFaved: false,
        isEdited: false,
        owner: 0
    }

    public add(column): void {
        const newId = column.tasks.length+1;
        const d = new Date();
        this.newTask.id = newId;
        this.newTask.timestamp = d.getFullYear() + "-" + d.getMonth() + "-" + d.getDay() + " " + d.getHours() + ":" + d.getMinutes() + ":" + d.getSeconds();
        this.newTask.owner = 0;
        column.tasks.push(this.newTask);    
        column.editing = !column.editing;
        this.newTask = {
            id: 0,
            title: "",
            timestamp: "",
            isFaved: false,
            isEdited: false,
            owner: 0
        }
    }

    public editing(column): void {
        column.editing = !column.editing;
        this.newTask = {
        id: 0,
        title: "",
        timestamp: "",
        isFaved: false,
        isEdited: false,
        owner: 0
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
.btn-display {
  width: 100%;
}
.card {
  background-color: rgb(235, 235, 235);
}
.smallcard {
  background-color: #fff;
  -webkit-box-shadow: 1px 1px 3px -1px rgba(0,0,0,0.62);
  -moz-box-shadow: 1px 1px 3px -1px rgba(0,0,0,0.62);
  box-shadow: 1px 1px 3px -1px rgba(0,0,0,0.62);
}
.card-header {
  background-color: #fff;
}
.card-footer {
  background-color: #fff;
}
</style>