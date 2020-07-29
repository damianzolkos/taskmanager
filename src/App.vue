<template>
    <div id="app">
        <select class="form-control select-user" v-model="selectedUser">
          <option v-for="user in users" v-bind:value="user.id" :key="user.id">
              {{user.name}}
          </option>
        </select>
        <div class="row">
          <draggable :animation="400" v-model="columns" group="columns" handle=".handle">
                <TasksList
                v-for="column in columns"
                :key="column.title"
                class="card bigcard d-inline-flex"
                :column = "column"
                :users = "users"
                :selected = "selectedUser"
                >
                </TasksList>
          </draggable>
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
    public users: Array<object> = [
          { 
            id: 0,
            name: "Wszyscy"
          },
          { 
            id: 1,
            name: "Jonh Doe",
            jobTitle: "Project Manager"
          },
          { 
            id: 2,
            name: "John Apple",
            jobTitle: "CEO"
          }
    ]

    public selectedUser = 0;

    public columns: Array<object> = [
        {
          title: "Do realizacji",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "Wyłączenie poszczególnych adresów",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: 0
            },
            {
              id: 2,
              title: "Płatność odroczona",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false,
              owner: 0
            },
            {
              id: 3,
              title: "Autyt SEO",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false,
              owner: 0
            }
          ]
        },
        {
          title: "Realizowane",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "wykresy edito - rozbudowa",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: 0
            }
          ]
        },
        {
          title: "Rozwiązane",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "Pole wyszukiwania w filtrach",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: 0
            },
            {
              id: 2,
              title: "Dane kontaktowe dla powiadomień",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: 0
            }
          ]
        },
        {
          title: "Wstrzymane",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "rabat na krzesła",
              timestamp: "2020-6-2 13:46:20",
              isFaved: false,
              isEdited: false,
              owner: 0
            }
          ]
        },
        {
          title: "Zakończone",
          editing: false,
          tasks: [
            {
              id: 1,
              title: "Poprawa listingu",
              timestamp: "2020-6-2 13:46:20",
              isFaved: true,
              isEdited: false,
              owner: 0
            }
          ]
        }
    ]
}

</script>

<style>
html, body {
  background-color: rgb(29, 97, 141);
  min-height: 100%;
}
#app {
  padding: 40px 30px 0px 30px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: rgb(29, 97, 141);
}
#app > .row {
  overflow-x: auto;
  white-space: nowrap;
  display: block;
  min-height: 100% !important;
  padding: 5px;
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
.select-user {
  max-width: 300px;
}
</style>
