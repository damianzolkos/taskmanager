<template>
    <div>
    <input v-if="task.isEdited" type="text" v-model="task.title" class="taskTitleInput"/>
    <p v-else class="taskTitle font-weight-normal">{{task.title}}</p>
        <select class="select-user" v-model="task.owner">
            <option disabled value="">Przypisz do używkownika: </option>
            <option v-for="user in filteredUsers()"
                :key="user.id"
                v-bind:value="user.id">
                
                <span v-if="user.id!=0">{{user.first_name}} {{user.last_name}} - {{user.job_title}}</span>
                <span v-else>{{user.first_name}}</span>
            </option>
        </select>
        <div class="m-0 p-0">
            <p class="timestamp text-muted p-0 m-0">{{task.timestamp}}</p>
            <div @click="edit(task)" class="smallButton">
                <b-icon-pencil-square></b-icon-pencil-square>
            </div>
            <div @click="fav(task)" class="smallButton">
                <b-icon-star></b-icon-star>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Task extends Vue {
    @Prop() private task!: object;
    @Prop() private users;

    public edit(task): void {
        task.isEdited = !task.isEdited;
    }

    public fav(item): void {
        item.isFaved = !item.isFaved;
    }

    public filteredUsers() {
        return this.users.filter(user => user.job_title != null);
    }
}

</script>

<style scoped>

.taskTitle {
  margin: -5px -5px 5px -5px;
  padding: 3px 5px;
  position: relative;
  border: 1px solid #fff;
  max-width: calc(100% + 10px);
  background-color: #fff;
  word-break: break-word;
  white-space: normal;
}
.taskTitleInput {
  margin: -5px -5px 5px -5px;
  padding: 3px 5px;
  max-width: calc(100% + 10px);
  background-color: #fff;
  border: 1px solid rgb(194, 194, 194);
  border-radius: 2px;
}
.timestamp {
  display: inline-block;
  width: 80%;
  font-size: 8pt;
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
    margin: 3px -5px 3px -5px;
    border: 1px solid #fefefe;
    font-size: 9pt;
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