<script lang="ts">
	import { createEventDispatcher } from "svelte";

	let ev = createEventDispatcher();

	export let tx: string;
	function click(){
		ev('resposta', {
			resposta: tx
		});
	}
</script>

	<button on:click="{() => click()}">{tx}</button>

<style>
	button {
		width: 18vw;
		height: 18vw;
		margin: 4px;
	}
</style>