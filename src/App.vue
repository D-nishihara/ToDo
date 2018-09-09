<template>
  <div id="app">
      <h1>ToDoリスト</h1>
      <input type="text" v-model="textinput" placeholder="タスクを入力">
      <input type="button" v-on:click="insertbutton" value="登録">
      <p class="p-position"><span>{{textinput.length}}</span>文字</p>
      <div class="div-position" v-for="(todo,idx) in todolist" v-bind:key="(todo,idx)">
        <input type="checkbox" id="check" v-model="todo.checke">
        <label for="check">{{todo.name}}</label>
        <input type="button" v-on:click="deleatebutton(todo,idx)" value="削除">
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textinput: '',
      todolist: [],
    };
  },
  methods: {
    insertbutton() {
      if (this.textinput === '') return;
      this.todolist.push({ name: this.textinput, checke: false });
      this.textinput = '';
    },
    deleatebutton(todo, idx) {
      if (todo.checke === true) {
        this.todolist.splice(idx, 1);
      } else {
        return;
      }
    },
  },
};

</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
.p-position {
  font-size: 80%;
  margin-top: 0px;
  position: absolute;
  left: 380px;
}
.div-position {
  padding-top: 25px
}

</style>
