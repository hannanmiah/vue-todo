<template>
	<div
		class="
			absolute
			w-full
			h-screen
			top-0
			right-0
			flex
			justify-center
			items-center
			transparent
		"
	>
		<div class="max-w-md bg-white rounded-lg">
			<div class="p-4 border-b-2">
				<h1 class="text-black font-bold" v-if="mode === 'edit'">
					Edit {{ todo.name }}
				</h1>
				<h1 v-else-if="mode === 'remove'">
					Are you sure? Remove {{ todo.name }}?
				</h1>
				<h1 v-else>Default title</h1>
			</div>
			<div v-if="mode === 'edit'" class="p-4">
				<input
					v-model="selectedTodo.name"
					type="text"
					class="w-full border-2 border-gray-200 p-2"
				/>
			</div>
			<div class="p-4 border-t-2 flex justify-end items-center space-x-2">
				<button @click="emit('removed',selectedTodo)" v-if="mode === 'remove'" class="p-2 bg-red-500 rounded">
					Remove
				</button>
				<button @click="emit('updated',selectedTodo)" v-if="mode === 'edit'" class="p-2 bg-green-500 rounded">
					Update
				</button>
				<button
					@click="emit('toggle')"
					class="bg-yellow-500 p-2 rounded text-white"
				>
					Close
				</button>
			</div>
		</div>
	</div>
</template>

<script setup>
	import { reactive } from "vue";

	const props = defineProps({
		mode: String,
		todo: Object,
	});

	const selectedTodo = reactive({
		id: props.todo.id,
		name: props.todo.name,
		done: props.todo.done
	})

	const emit = defineEmits(["toggle", "updated", "removed"]);
	
</script>

<style scoped>
	.transparent {
		background: rgba(0, 0, 0, 0.5);
	}
</style>