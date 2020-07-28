<template>
    <div id="app">
      <div class="board">
        <div class="row">
              <draggable :animation="200" group="categories" handle=".handle">
                <div
                v-for="column in columns"
                :key="column.title"
                class="card bigcard d-inline-flex w-200"
                >
            
                  <h5 class="card-header handle">{{column.title}}</h5>

                  <draggable :list="column.tasks" :animation="200" ghost-class="ghost-card" group="tasks">
                    <div
                      v-for="(task) in column.tasks"
                      :key="task.id"
                      :task="task"
                      class="card smallcard"
                      v-bind:class="{ faved: task.isFaved }"
                      >
                      <p v-if="!task.isEdited" class="taskTitle">{{task.title}}</p>
                      <input v-else type="text" v-model="task.title" class="taskTitleInput"/>

                      <div class="buttons-container">
                          <p class="timestamp">{{task.timestamp}}</p>
                          <div @click="edit(task)" class="smallButton">
                            <b-icon-pencil-square></b-icon-pencil-square>
                          </div>
                
                          <div @click="fav(task)" class="smallButton">
                            <b-icon-star></b-icon-star>
                          </div>
                      </div>

                    </div>
                  </draggable>
                  <div 
                  v-if="column.editing"
                  >
                  <input type="text" v-model="newTask.title" placeholder="" class="newinput"/>
                  <button type="button" @click="add(column)" class="btn btn-light btn-sm w-50"><b-icon-check2 variant="success"></b-icon-check2></button>
                  <button type="button" @click="editing(column)" class="btn btn-light btn-sm w-50" ><b-icon-x-circle-fill variant="danger"></b-icon-x-circle-fill></button>
                  </div>
                  <button v-else type="button" @click="editing(column)" class="btn btn-light"><b-icon-plus></b-icon-plus></button>
                </div>
              </draggable>
        </div>
      </div>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import draggable from "vuedraggable";

import { BIconStar, BIconPencilSquare, BIconPlus, BIconCheck2, BIconXCircleFill} from 'bootstrap-vue'

Vue.component('BIconXCircleFill', BIconXCircleFill)
Vue.component('BIconCheck2', BIconCheck2)
Vue.component('BIconPlus', BIconPlus)
Vue.component('BIconStar', BIconStar)
Vue.component('BIconPencilSquare', BIconPencilSquare)

@Component({
  components: {
    draggable
  }
})

export default class App extends Vue {
  public newTask: Record<string, any> = {
    id: 0,
    title: "",
    timestamp: "",
    isFaved: false
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
      isFaved: false
    }
  }

  public editing(column): void {
    column.editing = !column.editing;
  }

  public edit(task): void {
    task.isEdited = !task.isEdited;
  }


  public fav(item): void {
    item.isFaved = !item.isFaved;
  }

    private columns: Array<object> = [
        {
          title: "jeden",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "zrobić rzecz",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false
            },
            {
              id: 2,
              title: "kupić rzeczy",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false
            },
            {
              id: 3,
              title: "ogarnąć życie",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false
            }
          ]
        },
        {
          title: "dwa",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "zjeść obiad",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false
            },
            {
              id: 2,
              title: "kupić kebzille w nagrodę",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false
            }
          ]
        },
        {
          title: "Trzy",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "zjeść obiad",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false
            },
            {
              id: 2,
              title: "zwalić konia",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false
            }
          ]
        },
        {
          title: "cztery",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "zrobić obiad",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false
            },
            {
              id: 2,
              title: "zjeść cukinie",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false
            }
          ]
        },
        {
          title: "Pięć",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "zjeść obiad",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false
            },
            {
              id: 2,
              title: "obejrzeć serialiks",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false
            }
          ]
        }
    ]
}

</script>

<style>
#app {
  margin-top: 50px;
  margin-left: 20px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.category {
  margin-top: 20px;
  padding: 10px;
}
.faved{
  border-left: 3px solid red !important;
  padding: 10px 10px 10px 8px !important;
}
.w-200{
    width: 250px !important;
}
.bigcard {
  margin: 10px;
}
.smallcard {
  padding: 10px;
  margin: 10px;
}

draggable {
  display: inline-block;
}
.newinput {
  width: calc(100% - 20px);
  position: relative;
  margin: 10px;
}
.taskTitle {
  margin: 0px;
  padding: 0px;
  border: 1px solid #fff;
  max-width: 100%;
  background-color: #fff;
}
.taskTitleInput {
  margin: 0px;
  padding: 0px;
  border: 1px solid #111;
  max-width: 100%;
  background-color: #fff;
}
.buttons-container {
  padding: 0px;
  margin: 10px 0px 0px;
}
.timestamp {
  display: inline-block;
  width: 80%;
  font-size: 8pt;
  padding: 0px;
  margin: 0px;
}
.smallButton {
  cursor: pointer;
  display: inline-block;
  width: calc(10% - 10px);
  padding: 0;
  margin: 0px 5px;
}
</style>
