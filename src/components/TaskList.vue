<template id="task-list">
  <section class="tasks">
    <h1>
      Tasks 
      <transition name="fade">
        <small v-if="incomplete" class="text-secondary">({{ incomplete }})</small>
      </transition>
    </h1>
    <b-input-group class="tasks__new pt-3">
      <b-form-input type="text"
              class="input-group-field"
              v-model="newTask"
              @keyup.enter="addTask"
              placeholder="New task"
      />
      <b-input-group-append class="input-group-button">
        <b-button @click="addTask" class="text-light" variant="primary" squared>
          <i class="fa fa-plus"></i> Add
        </b-button>
      </b-input-group-append>
    </b-input-group>

    <div class="tasks__clear float-right mt-3">
      <b-button variant="warning" class="text-light" @click="clearCompleted" squared>
        <i class="fa fa-check"></i> Clear Completed
      </b-button>
      <b-button variant="danger" class="text-light ml-1" @click="clearAll" squared>
        <i class="fa fa-trash"></i> Clear All
      </b-button>
    </div>
    
    <transition-group name="fade" tag="ul" class="tasks__list pt-3">
        <task-item v-for="(task, index) in tasks"
                    @remove="removeTask(index)"
                    @complete="completeTask(task)"
                    :task="task"
                    :key="task.id"
        />
    </transition-group>
  </section>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import TaskItem from './TaskItem.vue';

export interface Task {
  id: string;
  title: string;
  completed: boolean;
}

@Component({
  components: {
    'task-item': TaskItem,
  },
})
export default class TaskList extends Vue {
  public tasks: Task[] = [];
  public newTask: string = '';
  get incomplete() {
    return this.tasks.filter(this.inProgress).length;
  }
  public addTask(): void {
    const trimValue = this.newTask.replace(/ /gi, '');
    if (trimValue.length) {
      this.tasks.push({
        id: 'task-' + new Date().getTime(),
        title: this.newTask,
        completed: false,
      });
      this.newTask = '';
    }
  }
  public clearCompleted(): void {
    this.tasks = this.tasks.filter(this.inProgress);
  }
  public clearAll(): void {
    this.tasks = [];
  }
  public removeTask(index: number): void {
    this.tasks.splice(index, 1);
  }
  public completeTask(task: Task): void {
    task.completed = !task.completed;
  }
  private inProgress(task: Task) {
    return !this.isCompleted(task);
  }
  private isCompleted(task: Task) {
    return task.completed;
  }
}
</script>

<style scoped>
  .tasks {
    width: 100%;
    max-width: 30rem;
    padding: 2em;
    margin: 2em auto;
    overflow: auto;
    background-color: white;
    box-shadow: 0px .25rem 1rem rgba(black, .25);
  }
  .tasks__list {
    clear: both;
  }
</style>
