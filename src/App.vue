<template>
    <div id="app">
      <div class="container">
              <draggable :animation="200" group="categories" class="">
                <div
                v-for="column in columns"
                :key="column.title"
                class="card bigcard d-inline-flex"
                >
            
                  <h5 class="card-header">{{column.title}}</h5>

                  <draggable :list="column.tasks" :animation="200" ghost-class="ghost-card" group="tasks">
                    <div
                      v-for="(task) in column.tasks"
                      :key="task.id"
                      :task="task"
                      class="card smallcard"
                      v-bind:class="{ faved: task.isFaved }"
                      >
                      {{task.title}}
                      <br>
                      {{task.timestamp}}
                    </div>
                  </draggable>
                  
                  <button type="button" class="btn btn-secondary">+</button>
                </div>
              </draggable>
      </div>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import draggable from "vuedraggable";

@Component({
  components: {
    draggable
  }
})

export default class App extends Vue {
    private columns: Array<object> = [
        {
          title: "jeden",
          tasks: [
            {
              id: 1,
              title: "zrobić rzecz",
              timestamp: "1595923797",
              isFaved: false
            },
            {
              id: 2,
              title: "kupić rzeczy",
              timestamp: "765676800",
              isFaved: true
            },
            {
              id: 3,
              title: "ogarnąć życie",
              timestamp: "672351872",
              isFaved: false
            }
          ]
        },
        {
          title: "dwa",
          tasks: [
            {
              id: 6,
              title: "zjeść obiad",
              timestamp: "765676800",
              isFaved: true
            },
            {
              id: 7,
              title: "kupić pierścionek",
              timestamp: "672351872",
              isFaved: false
            }
          ]
        },
        {
          title: "Trzy",
          tasks: [
            {
              id: 6,
              title: "zjeść obiad",
              timestamp: "765676800",
              isFaved: true
            },
            {
              id: 7,
              title: "kupić pierścionek",
              timestamp: "672351872",
              isFaved: false
            }
          ]
        }
    ]
}

</script>

<style>
#app {
  margin-top: 50px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.category {
  margin-top: 20px;
  padding: 10px;
}
.categorytitle {
  margin-top: 20px;
  text-decoration: underline
}
.faved {
  border-left: 3px solid red;
}
.bigcard {
  width: 300px;
  margin: 10px;
}
.smallcard {
  padding: 10px;
  margin: 10px;
}
draggable {
  display: inline-block;
}
</style>
