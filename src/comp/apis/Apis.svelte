<script lang="ts">
	import Flex from "../estilo/Flex.svelte";
	let inp = 'https://swapi.dev/api/people/1/';
	let api : Promise<any>;
	let resp: string = '';

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
		const response = await fetch(url);
		const todo = await response.json();

		if (response.ok) {
			return todo;
		} else {
			throw new Error(todo);
		}
	}

	function print(v){
		v = JSON.stringify(v, null, '\t');
		return v;
	}

</script>

<main>
	<form on:submit|preventDefault="{submit}">
		<Flex>
			<input type="text" bind:value="{inp}">
		</Flex>
	</form>
	<pre>
		{#if resp != ''}
			{#await api}
				<p>...waiting</p>
			{:then ret}
				{ print(resp) }
			{:catch error}
				<p style="color: red">{error}</p>
			{/await}
		{/if}
	</pre>
</main>

<style>
	pre { text-align: left; }
</style>