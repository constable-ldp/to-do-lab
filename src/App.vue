<template>
  <div id="app">

    <h2 class="title">To Do's</h2>

    <br>
    <form v-on:submit.prevent="saveNewItem">
      <label for="new-item">Add New Item:</label>
      <input type="text" id="new-item" v-model="newItem.name" required>
      <input type="radio" @change="chooseLowToTrue" v-model="newItem.priority" id="chooselow" name="choosehighlow" v-bind:value=false>
      <label for="chooselow">Low</label>
      <input type="radio" @change="chooseHighToTrue" v-model="newItem.priority" id=choosehigh name="choosehighlow" v-bind:value=true>
      <label for="choosehigh">High</label>
      <input type="submit" value="Save Item">
    </form>

    <!-- <h2 class="title">Highlight</h2> -->
    <br>
    <div class="highlight">
      <input type="radio" @change="lowToTrue" v-model="high" id="low" name="highlow" checked>
      <label for="low">Highlight Low</label>
      <br>
      <br>
      <input type="radio" @change="highToTrue" v-model="high" id="high" name="highlow">
      <label for="high">Highlight High</label>
    </div>

    <h2 class="title">To-Do List</h2>
    <div class="container">
      <div class="item" v-for="item, index in todo_list" v-bind:key="index">
        <span v-bind:class="high===item.priority ? 'highlighted' : 'notHighlighted'">{{item.name}}</span>
        <button v-if="item.priority" @click="changeToLow(index)">Change to Low</button>
        <button v-else @click="changeToHigh(index)">Change to High</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      // note: true = high priority, fasle = low priority
      todo_list: [
        {name: "Buy Shopping", priority: true},
        {name: "Clean Bathroom", priority: false},
        {name: "Car's MOT", priority: true}
      ],
      newItem: {name: "", priority: false},
      high: false,
    }
  },

  methods: {
    saveNewItem: function(){
      this.todo_list.push(this.newItem);
      this.newItem = {name: "", priority: false};
    },

    changeToHigh: function(index){
      this.todo_list[index].priority = true;
    },

    changeToLow: function(index){
      this.todo_list[index].priority = false;
    },

    lowToTrue: function(){
      this.high = false;
    },

    highToTrue: function(){
      this.high = true;
    },

    chooseLowToTrue: function(){
      this.priority = false;
    },

    chooseHighToTrue: function(){
      this.priority = true;
    },

  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-flow: column wrap;
  text-align: center;
  text-decoration: center;
  list-style: none; 
}

.title {
  text-align:center;
}

.highlighted {
  color: red;
}

.highlight {
  padding: 20px;
}

.item {
  align-self: auto;
  margin: 2%;
}
</style>
