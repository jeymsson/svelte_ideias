<script lang="ts">
	import Flex from '../estilo/Flex.svelte';
	import Linha from '../estilo/Linha.svelte';
	import Get from './Get.svelte';
	import Post from './Post.svelte';
	let api_value;
	let resp: string = '';
	let api : Promise<any>;
</script>

<main>

	<Flex>
		<Linha>
			<select bind:value="{api_value}">
				<option value="1">get</option>
				<option value="2">post</option>
			</select>
			{#if api_value == 1}
				<Get bind:resp={resp} bind:api={api}  />
			{:else if api_value == 2}
				<Post bind:resp={resp} bind:api={api} />
			<!-- {:else} -->
			{/if}
		</Linha>
		<Linha>
			<pre>
				{#if resp != ''}
					{#await api}
						<p>...waiting</p>
					{:then ret}
						<!-- { print(resp) } -->
						{JSON.stringify(resp, null, '\t')}
					{:catch error}
						<p style="color: red">{error}</p>
					{/await}
				{/if}
			</pre>
		</Linha>
	</Flex>

</main>

<style>
	pre { text-align: left; }
	input { width: 100%; margin: auto; }
</style>
