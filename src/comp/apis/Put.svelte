<script lang="ts">
	import Flex from "../estilo/Flex.svelte";
	import Linha from "../estilo/Linha.svelte";
	export let api : Promise<any>;
	export let resp: string = '';
	let url = 'http://localhost:3000/api/contacts/27';
	let txa = '{ "id": 12, "name": "Berlin Oriental", "visited": 1, "lat": 52.52, "lng": 13.405}';

	function submit() {
		api = getTodo(url, txa)
			.then(c => {
				resp = c
			})
			.catch(e => {
				resp = JSON.parse(JSON.stringify({ erro: e }, null, '\t'));
			});
	}

	async function getTodo(url: string, txa: string) {
		const response = await fetch(url, {
			method: "PUT",
			body: (txa === "object" ? JSON.stringify(txa) : txa),
			headers: {"Content-type": "application/json; charset=UTF-8"}
		})

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
			<input type="text" bind:value="{url}">
		</Linha>
		<Linha>
			<textarea 
				placeholder="Json"
                bind:value={txa}
			></textarea>
		</Linha>
	</Flex>
</form>

<style>
	form { width: 100%; }
	input { width: 100%; margin: auto; }
	textarea { width: 100%; }
</style>


