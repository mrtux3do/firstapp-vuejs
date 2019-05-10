<template id="task-list">
	<div class="wrapper">
		<input type="text" name="todo" v-model="newTask" @keyup.enter="addTask"><button class="btn-button" v-on:click="addTask">Add task</button>
		<button class="btn-button" v-on:click="removeAll">Del All Task</button>
		<div class="task" v-for="(task, index) in tasks"  :class="{done: isChecked(task)}">
			<div class="bg-checkbox"> <input type="checkbox" name="checked" v-model="task.checked" v-on:click="check(task)"></div><span >{{ task.text }}</span> <button class="btn-button" v-on:click="removeTask(index)">del</button>
		</div>
	</div>
</template>

<script>
	import todoTask from './todoTask.vue';
	export default {
		components: {
			todoTask
		},

		data() {
			return {
				newTask: "",
				tasks: [{
					text: "This is example task",
					checked: false
				}],
			}
		},

		methods: {
			addTask: function(){
				if (this.newTask) {
					this.tasks.push({
						text: this.newTask,
						checked: false
					});
					this.newTask = '';
				}
			},
			removeTask: function(index){
				this.tasks.splice(index, 1);
			},
			check: function(task){
				task.checked = true;
			},
			isChecked: function (task) {
				return task.checked;
			},
			removeAll: function(){
				this.tasks = [];
			}
		}
	};
</script>

<style type="text/css">
	.done span{
		text-decoration: line-through;
		vertical-align: middle;
		color: black !important;
	}
	input[type="text"]{
		width: 450px;
		height: 50px;
		border: 1px solid #72c5c9;
		border-radius: 3px;
		margin-right: 5px;
		padding-left: 30px;
	}
	.btn-button{
		height: 52px;
		padding: 0 20px;
		background: #72c5c9;
		border-radius: 3px;
		border: none;
		text-transform: uppercase;
		color: #fff;
		cursor: pointer;
	}
	.wrapper{
		text-align: left;
	}
	input[type="checkbox"]{
		height: 20px;
		vertical-align: middle;
		width: 20px;
		margin: 16px;
	}
	.task{
		margin-top: 20px;
	}

	.task span{
		background: #72c5c9;
		padding: 18px;
		color: #fff;
		vertical-align: middle;
		border-top-right-radius: 3px;
		border-bottom-right-radius: 3px;
	}
	.bg-checkbox{
		display: inline-block;
		width: 50px;
		height: 53px;
		vertical-align: middle;
		background: #72c5c9;
	}
</style>