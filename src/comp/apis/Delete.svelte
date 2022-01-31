<script lang="ts">
	import Flex from "../estilo/Flex.svelte";
	import Linha from "../estilo/Linha.svelte";
	export let api : Promise<any>;
	export let resp: string = '';
	let inp = 'http://localhost:3000/api/contacts/31        ';

	function submit() {
		api = getTodo(inp)
			.then(c => {
				resp = c
			})
			.catch(e => {
				resp = JSON.parse(JSON.stringify({ erro: e }, null, '\t'));
			});
	}

	async function getTodo(url: string) {
		const response = await fetch(url, {
			method: "DELETE",
			headers: {"Content-type": "application/json; charset=UTF-8"}
		});
		const todo = await response.json();

		if (response.ok) {
			return todo;
		} else {
			throw new Error(todo);
		}
	}

</script>

<form on:submit|preventDefault="{submit}">
	<Flex>
		<Linha>
			<input type="text" bind:value="{inp}">
		</Linha>
	</Flex>
</form>

<style>
	form { width: 100%; }
	input { width: 100%; margin: auto; }
</style>
