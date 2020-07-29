<template>
    <div id="app">
        <select class="form-control-sm select-user" v-model="selectedUser">
          <option v-for="user in users" v-bind:value="user.id" :key="user.id">
              <span v-if="user.id!=0">{{user.first_name}} {{user.last_name}} <span v-if="user.job_title!=null">- {{user.job_title}}</span> </span>
              <span v-else>{{user.first_name}}</span>
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
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

@Component({
  components: {
    draggable,
    TasksList
  }
})
export default class App extends Vue {

    public users: Array<object> = []
    public selectedUser = 0;

    mounted() {
      axios
        .get('https://www.mocky.io/v2/5e0de1893300002b00aa88f3')
        .then(response => {
          this.users.push({
            id: 0,
            job_title: "", // eslint-disable-line
            first_name: "Wszyscy" // eslint-disable-line
          })
          response.data.forEach(element => {
            this.users.push(element)
          });
        })
    }

    public columns: Array<object> = [
        {
          title: "Do realizacji",
          id: 1,
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
          id: 2,
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
          id: 3,
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
          id: 4,
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
          id: 5,
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
  background-color: rgb(29, 97, 141) !important;
  width: 100%;
  height: 100%;
  overflow-x: auto;
  white-space: nowrap;
  display: block;
}
#app {
  padding: 40px 30px 0px 30px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.category {
  margin-top: 20px;
  padding: 10px;
}
.bigcard {
  margin: 10px;
  width: 230px !important;
}
.select-user {
  max-width: 300px;
  margin-left: -5px;
  margin-bottom: 20px;
}
</style>
