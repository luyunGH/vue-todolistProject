<template>
	<div id="app">
		<h1 v-text="msg"></h1>
		<input type="text" v-model="newItem" v-on:keyup.enter="addNew">
		<ul>
			<li 
			v-for="(item,index) in items" 
			v-bind:class="{finished:item.isFinished}" 
			v-on:click="toggleFinish(item)" :key='index'>
			{{item.label}}
			</li>
		</ul>
		<p>儿子传给我的信息： {{ childMsg }}</p>
		<!-- 父传子信息 -->
		<component-a msgfromfather="this is父传给儿子的information"
		v-on:child-tell-me-something='listenToMyBoy'></component-a>
	</div>
</template>

<script>
import Store from './store'
import ComponentA from './components/componentA'
export default {
  	// name: 'App'
	components: { ComponentA },
  	data () {
    	return {
      		msg: 'this is a todo list',
      		items: Store.fetch(),
			newItem: '',
			childMsg: ''
    	}
  	},
	methods: {
		toggleFinish: function (item) {
			item.isFinished = !item.isFinished;
		},
		addNew: function () {
			this.items.push({
				label:this.newItem,
				isFinished:false
			})
			this.newItem="";
		},
		listenToMyBoy: function (msg) {
			this.childMsg = msg;
		}
	},
	watch: {
		// 观察 每次对items数组进行改变时都会执行handler函数
		items:{
		handler:function (items) {
			Store.save(items);
		},
		deep:true
		}
	}
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
