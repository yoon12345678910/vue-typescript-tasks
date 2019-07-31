<template>
  <div id="app">
    <task-list />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import TaskList from './components/TaskList.vue';
import BootstrapVue from 'bootstrap-vue';

Vue.use(BootstrapVue);

@Component({
  components: {
    'task-list': TaskList,
  },
})
export default class App extends Vue {
}
</script>

<style lang="scss">

@import "node_modules/bootstrap/scss/bootstrap";
@import "node_modules/bootstrap-vue/src/index.scss";
@import url('https://fonts.googleapis.com/css?family=Nunito&display=swap');

body {
  background-color: #abc;
}
*, h1, button {
  font-family: 'Nunito', sans-serif;
}
ol, ul, li {
  list-style: none;
  padding: 0;
  margin: 0;
}
.btn:focus {
  box-shadow: none;
  outline: none;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-active {
  opacity: 0;
}

</style>
