<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{ finished:item.isFinished }" v-on:click="toggleFinished(item)">{{ item.label }}</li>
    </ul>
  </div>
</template>

<script>
export default {
    data:function () {
      return{
        title:'This is a todo list!',
        items:[
           {
             label:'cording',
             isFinished:false,
           },
           {
             label:'cooking',
             isFinished:true,
           }
        ],
        newItem :''
      }
    },
  methods:{
        toggleFinished:function (item) {
          item.isFinished = !item.isFinished
        },
        addNew:function () {
          this.items.push({
            label:this.newItem,
            isFinished:false,
          }),
          this.newItem = ''
        }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished{
  text-decoration: underline;
}
</style>
