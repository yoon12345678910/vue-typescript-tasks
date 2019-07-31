<template id="task-item">
  <li class="tasks__item">
    <b-button-group class="w-100">
      <b-button :class="className" @click.self="$emit('complete')" squared class="text-dark">
        {{ task.title }}
      </b-button>
      <b-button class="tasks__item__remove" variant="danger" @click="$emit('remove')" squared>
        <i class="fa fa-times"></i>
      </b-button>
    </b-button-group>
  </li>
</template>


<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import { Task } from './TaskList.vue';

@Component
export default class TaskItem extends Vue {
  @Prop() public task!: Task;

  get className() {
    const classes = ['tasks__item__toggle'];
    if (this.task.completed) {
      classes.push('tasks__item__toggle--completed');
    }
    return classes.join(' ');
  }
}
</script>

<style scoped>
  .tasks__item {
    position: relative;
    margin-bottom: .5em;
    border: 0;
  }
  .tasks__item__toggle {
    width: 100%;
    padding: .85em 2.25em .85em 1em;
    border: 1px solid rgba(0, 0, 0, .1);
    background-color: rgba(0, 0, 0, 0.05);
    text-align: left;
    cursor: pointer;
  }
  .tasks__item__toggle:hover {
    background-color: rgba(0, 0, 0, 0.1);
    border-color: rgba(0, 0, 0, 0.15);
  }
  .tasks__item__toggle--completed {
    text-decoration: line-through !important;
    background-color: rgba(0, 128, 0, 0.15);
    border-color: rgba(0, 128, 0, 0.2);
  }
  .tasks__item__toggle--completed:hover {
    background-color: rgba(0, 128, 0, 0.25);
    border-color: rgba(0, 128, 0, 0.3);
  }
</style>
