<template>
  <div id="app">
      <div class="leftflex">
  
      </div>
      <div class="contets">
          <h1>ToDoリスト</h1>
          <input type="text" v-model="textinput" placeholder="タスクを入力">
          <input type="button" v-on:click="insertbutton" value="登録">
          <p class="p-position"><span>{{textinput.length}}</span>文字</p>
          <div class="div-position" v-for="todo in todolist" v-bind:key="(todo)">
            <label class="todo-style">
                <input type="checkbox" v-model="todo.check">
                <template v-if="todo.edit">
                    <input type="text" v-model="todo.name" v-on:mouseout="textchange(todo)">
                </template>
                <template v-else>
                    {{todo.name}}
                </template>
                <input type="button" v-on:click="deletebutton(todo)" value="削除">
                <input type="button" v-on:click="changebutton(todo)" value="編集">
            </label>
          </div>
      </div>
      <div class="rightflex">
      </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      textinput: '',
      changetextinput:'',
      todolist: [],
      apilist: [],
    };
  },
  //vueインスタンス作成時にjsonserverから値を取得する。
  //問題点:作成されるが内容が空の表示になってしまう。 2018/09/23
  /*created() {
    axios.get("http://localhost:3000/comments")
    .then( response => {this.todolist = response})
  },*/
  methods: {
    insertbutton() {
      if (this.textinput === '') return;
      this.todolist.push({ name: this.textinput, check: false, edit: false});
      axios.post("http://localhost:3000/comments",{
            name:this.textinput,
            check:false,
            edit:false
      })
      this.textinput = '';
    },
    deletebutton(todo) {
      if (todo.check === true) {
        this.todolist = this.todolist.filter( item => item != todo );
      }
    },
    changebutton(todo) {
        todo.edit = true;
    },
    textchange(todo) {
        todo.edit = false;
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
  display: flex;
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
  position: relative;
  left: -83px;
}
.div-position {
  padding-top: 25px
}
.todo-style {
  border-bottom: solid 1px;
}
.leftflex {
  height: auto;
  width: 300px;
  border-right: solid 1px gray;
  margin-right: 10px;
}
.contents {
  flex: 1;
}
.rightflex {
  height: auto;
  width: 300px;
  border-left: solid 1px gray;
  margin-left: 10px;
}
</style>
