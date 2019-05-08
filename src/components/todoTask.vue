<template id="task-list">
	<div class="wrapper">
		<input type="text" name="todo" v-model="newTask" @keyup.enter="addTask"><button v-on:click="addTask">Add task</button>
		<button v-on:click="removeAll">Del All Task</button>
		<div v-for="(task, index) in tasks"  :class="{done: isChecked(task)}">
			<input type="checkbox" name="checked" v-model="task.checked" v-on:click="check(task)"><span >{{ task.text }}</span> <button v-on:click="removeTask(index)">del</button>
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
	.done{
		text-decoration: line-through;
	}
</style>