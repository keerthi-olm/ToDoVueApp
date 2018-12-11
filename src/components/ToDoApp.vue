<template>
  <ul id="list">
    <li class="header"><h2 class="title">My to do list</h2></li>
    <li class="mainsmall">
      <input ref="newItem" placeholder="Add a new task..." />
    </li>
    <li class="button add"><button v-on:click="_handleAddItem">Add</button></li>
    <li class="button reset"><button v-on:click="_handleResetList">Reset</button></li>
    <li class="main" v-for="(item, index) in list" :key="index">
      <input :key="index+100"
        v-if="
          doneList.filter(function(val) {
            return val === index;
          }).length === 0 ||
            doneList.filter(function(val) {
              return val === index;
            }).length === undefined
        "
        class="checkbox"
        type="checkbox"
        :id="index"
        v-on:click="_handleUpdateDoneList"
      />
      <input :key="index+100"
        v-else
        class="checkbox"
        type="checkbox"
        :checked="true"
        :id="index"
        v-on:click="_handleUpdateDoneList"
      />

      <strike>{{ item }}</strike>
    </li>

    <li class="footer">
      <button class="remove" v-on:click="_handleRemoveDoneItems">Remove</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "ToDoApp",
  data() {
    return {
      list: ["Get up in the morning", "Brush my teeth"],
      doneList: [0]
    };
  },
  computed: {
    // Computed stuff goes here
  },
  methods: {
     init() {
       this.resetList=[...this.list];
       this.resetDoneList=[...this.doneList];
     },
    _handleAddItem() {
      var newItem = this.$refs.newItem;
      if (newItem.value === "") return;
      this.list.push(newItem.value);
      console.log(this.$refs.newItem.value);
      newItem.value = ""
    },
    _handleUpdateDoneList(e) {
      console.log(e.target.checked);
      let checkIfInDoneList = this.doneList.filter(function(val) {
        return val === parseInt(e.target.id);
      });

      if (checkIfInDoneList === undefined || checkIfInDoneList.length === 0) {
        // add to list
        this.doneList.push(parseInt(e.target.id));
        e.target.checked = true;
      } else {
        //delete from list
        let i = this.doneList.indexOf(parseInt(e.target.id));
        this.doneList.splice(i, 1);
        e.target.value = false;
      }
      console.log("donelist afterremove-->");
      console.log(this.doneList);
    },
    _handleRemoveDoneItems(e) {
      this.doneList.sort((a, b) => a - b);
      console.log(this.doneList);
      for (var i = this.doneList.length - 1; i >= 0; i--)
        this.list.splice(this.doneList[i], 1);

      console.log(this.list);
      this.doneList = [];
    },
     _handleResetList() {
      //  let newItem =this.refs.newItem.value;
      console.log("\n ***Reset Button Pressed... **");
    

      
      this.donelist=[...this.resetDoneList];
      this.list=[...this.resetList];
        console.log(
        "Reset handler will reset list to default values..." +
          JSON.stringify(this.donelist)
      );
    }

  },
  mounted(){
    this.init()
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.App {
  font-family: sans-serif;
  text-align: center;
  font-size: 1.5em;
}

.widget ul {
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
.main {
  flex: 1 100%;
}
.button {
  flex: 1;
}
.mainsmall {
  flex: 9;
}

.widget li {
  /*background: tomato;*/
  padding: 10px;
  width: 500px;
  // border: 3px solid rgba(0, 0, 0, 0.2);

  /*color: white;*/
  font-weight: bold;
  font-size: 0.8em;
  text-align: right;
}

.widget li.header,
.widget li.footer {
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

.widget li.mainsmall input {
  width: 100%;
  height: 100%;
}
.widget li.main {
  font-size: 1.1em;
  line-height: 1.2em;
  display: flex;
  align-items: center;
}

.widget .checkbox {
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
