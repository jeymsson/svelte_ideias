<script lang="ts">
	import Flex from '../estilo/Flex.svelte';
	import Linha from '../estilo/Linha.svelte';
	import Get from './Get.svelte';
	import Post from './Post.svelte';
	import Put from './Put.svelte';
	import Delete from './Delete.svelte';
	let api_value;
	let resp: string = '';
	let api : Promise<any>;
	$: style = api_value == 1 ? 'green' : 
				(api_value == 2 ? 'bluee' : 
					(api_value == 3 ? 'yello' : 'reddd'));
		// 
</script>

<!-- <main> -->

	<Flex>
		<Linha>
			<select bind:value="{api_value}" class="{style}">
				<option value="1" class="green" >GET</option>
				<option value="2" class="bluee" >POST</option>
				<option value="3" class="yello" >PUT</option>
				<option value="4" class="reddd" >DELETE</option>
			</select>
			{#if api_value == 1}
				<Get bind:resp={resp} bind:api={api}  />
			{:else if api_value == 2}
				<Post bind:resp={resp} bind:api={api} />
			{:else if api_value == 3}
				<Put bind:resp={resp} bind:api={api} />
			{:else if api_value == 4}
				<Delete bind:resp={resp} bind:api={api} />
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

<!-- </main> -->

<style>
	pre { text-align: left; }
	.green { background-color: #0aca0a; color: black; }
	.bluee { background-color: #0e20bb; color: white; }
	.yello { background-color: #f7f724; color: black; }
	.reddd { background-color: #f84646; color: white; }
</style>

