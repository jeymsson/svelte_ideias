<script lang="ts">
	import Flex from "./estilo/Flex.svelte";
	import Linha from "./estilo/Linha.svelte";
	let prop = {
		lembra: ''
	};
	let list = [{text: 'A'}, {text: 'B'}, {text: 'C'}, {text: 'D'}];
	function addList(el){
		list.push({text: el});
		updateState()
	}
	function updateState(){
		list = list;
	}
	function submit(){
		addList(prop.lembra);
	}
</script>

<main>

	<Flex>
		<!-- <Linha> -->
			<form on:submit|preventDefault={submit}>
				<Linha>
					<label for="lembra">
						Lembrar:
						<input type="text" id="lembra" placeholder="Adicionar" bind:value="{prop.lembra}">
					</label>
					<input type="submit" value="Adicionar">
				</Linha>
			</form>
		<!-- </Linha> -->

		<Linha>
			<ul>
				{#each list as li}
					<li>{li.text}</li>
				{/each}
			</ul>
		</Linha>
	</Flex>


</main>

<style>
</style>