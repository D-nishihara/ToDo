<template>
  <div id="app">
      <h1>ToDoリスト</h1>
      <input type="text" v-model="textinput" placeholder="タスクを入力">
      <input type="button" v-on:click="insertbutton" value="登録">
      <p class="p-position"><span>{{textinput.length}}</span>文字</p>
      <div class="div-position" v-for="(todo,idx) in todolist" v-bind:key="(todo)">
        <label>
            <input type="checkbox" id="check" v-model="todo.checke">
            <template v-if="todo.edit && todo.checke">
                <input type="text" v-model="changetextinput" v-on:change="textchange(todo)">
            </template>
            <template v-else>
                {{todo.name}}
            </template>
            <input type="button" v-on:click="deletebutton(todo)" value="削除">
            <input type="button" v-on:click="changebutton(todo)" value="編集">
        </label>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textinput: '',
      changetextinput:'',
      todolist: [],
    };
  },
  methods: {
    insertbutton() {
      if (this.textinput === '') return;
      this.todolist.push({ name: this.textinput, checke: false, edit: false});
      this.textinput = '';
    },
    deletebutton(todo) {
      if (todo.checke === true) {
        this.todolist = this.todolist.filter( item => item != todo );
      }
    },
    changebutton(todo) {
        todo.edit = true;
    },
    textchange(todo) {
        todo.name = this.changetextinput;
        this.changetextinput = '';
        todo.edit = false;
    }
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
