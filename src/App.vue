<template>
	<div id="app">
		<h1 style="margin-bottom: 100px;">Tarefas</h1>
		<p>Acompanhe seu progresso:</p>
		<TasksProgress :progress="progress"/>
		<NewTask @taskAdded="addTask" />
		<TaskGrid :tasks="tasks" @taskDeleted="deleteTask"
		@taskStateChanged="toggleTaskState"></TaskGrid>
	</div>
		
</template>

<script>
import TaskGrid from './components/TaskGrid.vue'
import NewTask from './components/NewTask.vue'
import TasksProgress from './components/TasksProgress.vue'


export default {
	components: {TaskGrid, NewTask, TasksProgress},
	data(){
		return {
			tasks: []
		}
	},
	computed: {
		progress() {
			const total = this.tasks.length;
			const done = this.tasks.filter(t => !t.pending).length;
			return Math.round(done / total * 100) || 0
		}
	},
	methods: {
		addTask (task) {
			const sameName = t=> t.name === task.name
			const reallyNew = this.tasks.filter(sameName).length == 0
			if (reallyNew && task.name != ''){
				this.tasks.push({
					name: task.name,
					pending: task.pending || true
				})
			}

		},

		deleteTask(i){
			this.tasks.splice(i, 1);
			
		},

		toggleTaskState (i){
			this.tasks[i].pending = !this.tasks[i].pending;

		}
	}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}

	h1 + p {
		font-size: 1.5rem;
		color: rgb(141, 246, 159);
	}
</style>
