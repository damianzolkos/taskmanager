<template>
    <div id="app">
      <div class="board">
        <div class="row">
          <draggable :animation="400" v-model="columns" group="columns" handle=".handle">
                <TasksList
                v-for="column in columns"
                :key="column.title"
                class="card bigcard d-inline-flex"
                :column = "column"
                >
                </TasksList>
          </draggable>
        </div>
      </div>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import draggable from "vuedraggable";
import TasksList from './components/TasksList.vue';

@Component({
  components: {
    draggable,
    TasksList
  }
})

export default class App extends Vue {
    public columns: Array<object> = [
        {
          title: "Realizowane",
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
          title: "Wstrzymane",
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
          title: "Do realizacji",
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
          title: "Rozwiązane",
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
          title: "Zakończone",
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

.row {
  height: 100%;
}
/* The heart of the matter */
.board > .row {
  overflow-x: auto;
  white-space: nowrap;
  display: block;
}
.category {
  margin-top: 20px;
  padding: 10px;
}
.faved{
  border-left: 3px solid red !important;
  padding: 10px 10px 10px 8px !important;
}
.bigcard {
  margin: 10px;
  width: 250px !important;
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
  border: 1px solid rgb(194, 194, 194);
  border-radius: 2px;
  display: block;
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
  max-width: 100%;
  background-color: #fff;
  border: 1px solid rgb(194, 194, 194);
  border-radius: 2px;
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
  width: calc(10% - 11px);
  padding: 0;
}
.smallButton:nth-child(even) {
  margin-right: 14px;
}
.smallButton:nth-child(odd) {
  margin-right: 0px;
}
.btn-display {
  width: 100%;
}
</style>
