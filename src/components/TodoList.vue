<template>
	<h1 class="font-bold text-xl text-center mt-10">
		Todo List app with vue 3 and tailwindcss
	</h1>

	<div class="my-4 max-w-xl mx-auto">
		<div class="flex flex-col space-y-2">
			<input
				v-model="todoText"
				@keyup.enter="addTodo"
				type="text"
				:class="{ 'focus:border-red-500': !todoText }"
				class="
					border-2 border-gray-200
					focus:ring-0
					focus:border-green-500
					p-2
				"
				placeholder="Enter Todo Name here"
			/>
			<button
				@click="addTodo"
				:disabled="todoText.length === 0"
				:class="{ 'cursor-not-allowed': !todoText, 'opacity-80': !todoText }"
				class="
					bg-green-500
					focus:outline-none
					active:bg-green-600
					p-4
					text-white
				"
			>
				Add Todo
			</button>
		</div>
		<transition-group tag="ul" name="list" class="flex flex-col space-y-2 mt-4" appear>
			<li
				:key="todo.id"
				v-for="todo in todos"
				class="p-2 border-2 border-gray-200 flex justify-between items-center"
			>
				<h1 class="text-black font-bold" :class="{ done: todo.done }">
					{{ todo.name }}
				</h1>
				<div class="flex justify-between items-center space-x-2">
					<input
						:value="todo.done"
						@click="toggleDone(todo)"
						type="checkbox"
						class="
							h-6
							w-6
							border-2
							rounded-lg
							text-green-500
							border-gray-200
							checked:bg-green-500
							focus:ring-green-500
							checked:border-transparent
						"
					/>
					<button class="bg-yellow-500 p-2 focus:outline-none rounded">
						Edit
					</button>
					<button
						@click="deleteTodo(todo)"
						class="bg-red-500 p-2 focus:outline-none active:bg-red-600 rounded"
					>
						Delete
					</button>
				</div>
			</li>
		</transition-group>
		<div
			v-if="isEmpty"
			class="mt-4 border-2 border-gray-200 p-10 text-center text-green-500"
		>
			Todo List is Empty!
		</div>
	</div>
</template>

<script setup>
	import { ref, computed } from "vue";

	const todoText = ref("");

	const todos = ref([]);
	const isEmpty = computed(() => todos.value.length === 0);

	function addTodo() {
		if(!todoText.value) return;
		todos.value.unshift({
			id: new Date().getMilliseconds(),
			name: todoText.value,
			done: false,
		});

		todoText.value = "";
	}

	function toggleDone(todo) {
		todo.done = !todo.done;
	}

	function deleteTodo(todo) {
		todos.value = todos.value.filter((tod) => tod != todo);
	}
</script>

<style scoped>
	.done {
		text-decoration: line-through;
	}

	.list-enter-to {
		opacity: 1;
		transform: scale(1);
	}
	.list-enter-from {
		opacity: 0;
		transform: scale(0.6);
	}
	.list-enter-active {
		transition: all 0.3s ease;
	}

	.list-leave-from {
		opacity: 1;
		transform: scale(1);
	}
	.list-leave-to {
		opacity: 0;
		transform: scale(0.6);
	}
	.list-leave-active {
		transition: all 0.3s ease;
	}
	.list-move {
		transition: all 0.3s ease;
	}
</style>    