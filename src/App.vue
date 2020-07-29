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
    public users: Array<object>

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
              isEdited: false,
              owner: String
            },
            {
              id: 2,
              title: "kupić rzeczy",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false,
              owner: String
            },
            {
              id: 3,
              title: "ogarnąć życie",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: String
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
              isEdited: false,
              owner: String
            },
            {
              id: 2,
              title: "kupić kebzille w nagrodę",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: String
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
              isEdited: false,
              owner: String
            },
            {
              id: 2,
              title: "zwalić konia",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: String
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
              isEdited: false,
              owner: String
            },
            {
              id: 2,
              title: "zjeść cukinie",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: String
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
              isEdited: false,
              owner: String
            },
            {
              id: 2,
              title: "zjeść cukinie",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: String
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
.board > .row {
  overflow-x: auto;
  white-space: nowrap;
  display: block;
}
.category {
  margin-top: 20px;
  padding: 10px;
}

.bigcard {
  margin: 10px;
  width: 250px !important;
}

.btn-display {
  width: 100%;
}
</style>
