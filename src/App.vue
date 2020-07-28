<template>
    <div id="app">
<draggable class="category" :animation="200" group="categories">
        <div
          v-for="column in columns"
          :key="column.title"
          class=""
        >
          <p class="categorytitle">{{column.title}}</p>
          <draggable :list="column.tasks" :animation="200" ghost-class="ghost-card" group="tasks">
             <div
              v-for="(task) in column.tasks"
              :key="task.id"
              :task="task"
              class="mt-3 cursor-move"
              v-bind:class="{ faved: task.isFaved }"
              >
            {{task.id}}: {{task.title}}
            <br>
            {{task.timestamp}}
            </div>
          </draggable>
        </div>
</draggable>
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
        }
    ]
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
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
  color: red;
}
</style>
