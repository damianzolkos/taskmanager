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
}

</script>

<style scoped>

</style>