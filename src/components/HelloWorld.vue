<template>
  <h1>{{ msg }}</h1>

  <button type="button" @click="state.count++">count is: {{ state.count }}</button>

  <div>
    <button class="px-4 py-2 my-4 rounded-lg bg-red-600 focus:outline-none hover:bg-red-800" @click="changeName">
      Change My Name
    </button>
  </div>

  <div class="bg-green-400 text-red-400 hover:bg-green-600 p-4 my-2">
    <h1>{{myCustom}}</h1>
  </div>
</template>

<script setup>
	import { defineProps, reactive, ref } from "vue";

	defineProps({
		msg: String,
	});

	const state = reactive({ count: 0 });

	const myCustom = ref("my name is Hannan Miah");

	function changeName() {
		myCustom.value = "My name is Sadikul Islam";
	}
</script>

<style scoped>
	a {
		color: #42b983;
	}
</style>
