<template>
    <div>
    <input v-if="task.isEdited" type="text" v-model="task.title" class="taskTitleInput"/>
        <p v-else class="taskTitle">{{task.title}}</p>
        <div class="buttons-container">
            <p class="timestamp">{{task.timestamp}}</p>
            <div @click="edit(task)" class="smallButton">
                <b-icon-pencil-square></b-icon-pencil-square>
            </div>

            <div @click="fav(task)" class="smallButton">
                <b-icon-star></b-icon-star>
            </div>
        </div>
                <select class="form-control-sm select-user" v-model="task.owner" name="cars" id="cars">
                            <option v-for="(user) in users"
                                :key="user"
                                :task="user">
                                {{user.name}}
                            </option>
                </select>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Task extends Vue {
  @Prop() private task!: object;

  public edit(task): void {
    task.isEdited = !task.isEdited;
  }

  public fav(item): void {
    item.isFaved = !item.isFaved;
  }

  private users: Array<object> = [
        { 
          name: "Jonh Doe",
          jobTitle: "Project Manager"
        },
        { 
          name: "Jonh Doe 2",
          jobTitle: "none"
        }
  ]
}

</script>

<style scoped>
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
.select-user {
    border: 1px solid #fefefe;
    padding: 0px;
    margin: 0px;
    font-size: 8pt;
}
.faved{
  border-left: 3px solid red !important;
  padding: 10px 10px 10px 8px !important;
}
.smallcard {
  padding: 10px;
  margin: 10px;
}
</style>