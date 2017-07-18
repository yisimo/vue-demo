<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew" placeholder="Add a todo">
    <ul>
      <li v-for="item in items" v-bind:class="{ finished:item.isFinished }" v-on:click="toggleFinished(item)">{{ item.label }}</li>
    </ul>
    <p>Chileren speak : {{ childWords }}</p>
    <component-a msgfromfather="You are handsome!" v-on:child-tell="listenToMe"></component-a>

    <!--绑定class-->
    <!--对象语法-->
    <!--<div v-bind:class="{active:isActive,'text-danger':hasError}"></div>-->
    <!--<div v-bind:class="classObject"></div>-->
    <!--数组语法-->
    <!--<div v-bind:class="[activeClass,errorClass]"></div>-->

    <!--绑定内联样式-->
    <!--对象语法-->
  <!--  <div v-bind:style="{color:activeColor,fontSize:fontSize+'px'}">Hello World!</div>-->
    <div v-bind:style="styleObject">Hello World!</div>

    <!--数组语法-->
    <div v-bind:style="[styleObject, classObject]">My name is yisimo!</div>

    <!--条件渲染-->
    <div v-if="Math.random()>0.5">Sorry</div>
    <div v-else>Not sorry</div>

  </div>
</template>

<script>
import Store from "./store"
import ComponentA from "./components/componentA.vue"
export default {
    data :function () {
      return{
        title:'This is a todo list!',
        items:Store.fetch(),
        newItem :'',
        childWords:'',
        /*isActive:true,
        hasError:false,*/

       /* classObject:{
         active:true,
         'text-danger':false,
         }*/

      /* isActive:true,
        error:null,*/

     /*   activeClass:'active',
        errorClass:'text-danger',*/

     /*activeColor:'red',
        fontSize:30,*/

        styleObject:{
          color:'red',
          fontSize:'30px',
        },
        classObject:{
            border:'1px solid #000'
        }

      }
    },
/*  computed:{
    classObject:function () {
      return {
        active : this.isActive && !this.error,
        "text-danger" : this.error && this.error.type === 'fatal'
      }
    }
  },*/
  components:{ ComponentA },
  watch:{
    items:{
        handler:function (items) {
          Store.save(items)
        },
      deep:true
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
        },
        listenToMe:function (msg) {
          this.childWords = msg
        }
  }
}
</script>

<style>
  *{
    font-size: 14px;
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input{
  text-indent: 1rem;
}
.finished{
  text-decoration: underline;
}
.active{
  width: 30rem;
  height: 10rem;
  background-color: #f60;
}
</style>
