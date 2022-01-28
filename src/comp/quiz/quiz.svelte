<script lang="ts">
	import Flex from "../../estilo/Flex.svelte";
	import Linha from "../../estilo/Linha.svelte";
	import QuizOp from "../quizOp.svelte";

	$: ob = qu.quizz[ posPer ];
	$: resultados = (!joga ? resultado() : []);

	let resp = [];
	const qu = {
		quizz: [
			{ corr: 0, opcs: [2, 3, 4, 1], quiz: "Quanto é 1+1" },
			{ corr: 2, opcs: [2, 3, 4, 1], quiz: "Quanto é 2+2" },
		],
	};

	let posPer = 0;
	let joga = true;

	function escolhas(ev) {
		let i =  qu.quizz[posPer].corr;
		let v =  ev.detail.resposta == qu.quizz[posPer].opcs[i];
		resp = [...resp, v];
		if(joga){
			posPer++;
		}
		joga = posPer < (qu.quizz.length);
	}
	function resultado() {
		let cer = resp.reduce((a, v) => Number(a) + Number(v), 0);
		return [cer, resp.length];
	}
</script>

<main>

	<Flex>
		{#if joga}
			<Linha>
				<h2>{ob.quiz}</h2>
			</Linha>
			<Linha>
				{#each ob.opcs as e}
					<QuizOp on:resposta="{escolhas}" tx="{ e.toString() }" />
				{/each}
			</Linha>
		{:else}
			<h2>Você acertou {resultados[0]} de {resultados[1]}.</h2>
		{/if}

	</Flex>

</main>
