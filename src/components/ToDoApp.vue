<template>
  <ul id="todo_widget">
    <li class="header"><h2 class="title">My to do list</h2></li>
    <li class="new_item"><input ref="newItem" placeholder="Add a new task..." /> </li>
    <li class="button add"><button v-on:click="_handleAddItem">Add</button></li>
    <li class="button reset"><button v-on:click="_handleResetList">Reset</button></li>
    <li class="todo_item" v-for="(item, index) in list" :key="index"><input class="checkbox" type="checkbox" onclick="_handleUpdateDoneList"/>{{item}}</li>
    <li class="footer"> <button class="remove" onClick="_handleRemoveDoneItems">Remove</button></li>
  </ul>
</template>

<script>
export default {
  name: "ToDoApp",
   data() {
  return { list: ['item1','item2'],doneList:[] };
  },
  methods: {
    init() {
         
       },
    _handleAddItem() {
        },
    _handleUpdateDoneList(e) {
         },
    _handleRemoveDoneItems(e) {
    },
     _handleResetList() {
    }
  

  },
  mounted(){
    this.init()
  }
};

</script>

<style scoped>
#todo_widget {
  font-family: sans-serif;
  text-align: center;
  font-size: 1.5em;
}

ul#todo_widget {
  padding: 0;
  margin: 0;
  list-style: none;
  height: 200px;

  -ms-box-orient: horizontal;
  display: -webkit-box;
  display: -moz-box;
  display: -ms-flexbox;
  display: -moz-flex;
  display: -webkit-flex;
  display: flex;

  -webkit-justify-content: space-around;
  justify-content: space-around;
  -webkit-flex-flow: row wrap;
  flex-flow: row wrap;
  -webkit-align-items: stretch;
  align-items: stretch;
}

.header,
.footer,
.todo_item {
  flex: 1 100%;
}
.button {
  flex: 1;
}
.add_reset_section, .new_item{
  flex: 9;
}

#todo_widget li {
  /*background: tomato;*/
  padding: 10px;
  width: 500px;
  // border: 3px solid rgba(0, 0, 0, 0.2);

  /*color: white;*/
  font-weight: bold;
  font-size: 0.8em;
  text-align: right;
}

#todo_widget li.header,
#todo_widget li.footer {
  text-align: center;
}

button {
  color: #fff;
  text-transform: uppercase;
  background: #ed3330;
  padding: 0.5vw;
  border-radius: 5px;
  display: inline-block;
  border: none;
  height: 100%;
}
button.remove {
  background-color: green;
  padding: 0.1em;
  height: ;
}

#todo_widget li.new_item input {
  width: 100%;
  height: 100%;
}
#todo_widget li.todo_item {
  font-size: 1.1em;
  line-height: 1.2em;
  display: flex;
  align-items: center;
}

.#todo_widget .checkbox {
  height: 1em;
  width: 1em;
  color: green;
  margin-right: 0.2em;
}

strike {
  text-decoration: none;
}

input:checked + strike {
  text-decoration: line-through;
  opacity: 0.5;
}
</style>