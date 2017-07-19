<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew" placeholder="Add a todo">
    <ol>
      <li v-for="item in items" v-bind:class="{ finished:item.isFinished }" v-on:click="toggleFinished(item)">{{ item.label }}</li>
    </ol>

    <hr>

    <p>Chileren speak : {{ childWords }}</p>
    <component-a msgfromfather="You are handsome!" v-on:child-tell="listenToMe"></component-a>

    <hr>

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

    <hr>

    <!--条件渲染-->
    <div v-if="Math.random()>0.5">Sorry</div>
    <div v-else>Not sorry</div>

    <hr>

    <!--方法事件处理器-->
   <button v-on:click="greet">Greet!</button>

    <!--用内联处理器方法-->
    <button v-on:click="say('Hi!')">Say Hi!</button>

    <br>
    <!--阻止单击事件冒泡-->
    <a href="#" v-on:click.stop="doThis">doThis</a>

    <!--阻止页面重新加载-->
    <form href="#" v-on:submit.prevent="onSubmit">onSubmit</form>

    <!--修饰符可以串联-->
    <a href="#" v-on:click.stop.prevent="doThat">doThat</a>

    <!--只有修饰符-->
    <form v-on:submit.prevent>只有修饰符</form>

    <!--添加事件侦听器时使用事件捕获模式-->
    <a href="#" v-on:click.capture="doThis">doThis...</a>

    <!--只当事件在该元素本身（而不是子元素）触发时触发回调-->
    <a href="#" v-on:click.self="doThis">doThisByMyself</a>

    <hr>

    <br>
    <!--表单控件-->
    <input type="text" v-model="message" placehlder="edit me">
    <p>Message is : {{ message }}</p>

   <!-- <text-area v-model="message" placeholder="add multiple lines"></text-area>
    <p style="white-space:pre">{{ message }}</p>-->

    <!--复选框-->
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox" >{{ checked }}</label>

  </div>
</template>

<script>
import Store from "./store"
import ComponentA from "./components/componentA.vue"
export default {
  data: function () {
    return {
      title: 'This is a todo list!',
      items: Store.fetch(),
      newItem: '',
      childWords: '',
      message:'',
      checked:{
        false:false,
      },
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
        fontSize:30,*/ styleObject:{
        color: 'red',
        fontSize: '30px',
      },
    /*  classObject: {
        border: '1px solid #000'
      },*/
      name: 'Vue.js',
    }
  }, /*  computed:{
    classObject:function () {
      return {
        active : this.isActive && !this.error,
        "text-danger" : this.error && this.error.type === 'fatal'
      }
    }
  },*/
  components:{ComponentA },
  watch:{
    items:{
        handler:function
          (items) {
          Store.save(items)
        }, deep:true
    }
  },

  methods:{
    toggleFinished: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew:function
      () {
      this.items.push({
        label:this.newItem,
        isFinished: false,
      }),
        this.newItem = ''
    },
    listenToMe: function (msg) {
          this.childWords = msg
    },
    greet: function (event) {
      alert('Hello '+this.name+' !');
      alert(event.target.tagName);
    },
    say:function (msg) {
      alert(msg);
    }
  }
}
</script>

<style>
  *{
    font-size: 14px;
    margin: 1rem;
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
