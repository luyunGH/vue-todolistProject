<template>
  <div id="app">
    <h1 v-text="msg"></h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" 
      v-on:click="toggleFinish(item)">{{item.label}}</li>
    </ul>
  </div>
</template>

<script>
import Store from './store';
console.log(Store);
export default {
  // name: 'App'
  data (){
    return {
      msg:'this is a todo list',
      items:Store.fetch(),
      newItem:'',
    }
  },
  watch:{
    //每次对items数组进行改变时都会执行handler函数
    items:{
      handler:function(items){
        Store.save(items);
      },
      deep:true
    }
  },
  methods:{
    toggleFinish:function(item){
      item.isFinished = !item.isFinished;
    },
    addNew:function(){
      this.items.push({
          label:this.newItem,
          isFinished:false
      })
      this.newItem="";
    }
  },
}
</script>

<style>
.finished{
  text-decoration: underline;
}
html{
  height: 100%;
}
body{
  display: flex;
  align-items:center;
  justify-content: center;
  height: 100%;
}
</style>
