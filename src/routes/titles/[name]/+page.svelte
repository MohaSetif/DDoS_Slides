<script lang="ts">
	import { titles } from '$lib/deck/titles';
	import { page } from '$app/stores';
	import Reveal from '$lib/deck/reveal.svelte';
	$: decodedLocation = $page.params.name;
	$: neigbors = findNeigbors($page.params.name);
	function findNeigbors(currentName: string) {
		const currentIndex = titles.indexOf(currentName);
		const neigbors = [titles[currentIndex - 1], titles[currentIndex + 1]];
		return neigbors;
	}
</script>

<div class="section">
	<div class="navbar">
		<a href="/">DDoS</a>
		<h4>{decodedLocation}</h4>
		<div>
			{#if neigbors[0]}
				<a href="/titles/{neigbors[0]}">Previous</a>
			{/if}
			{#if neigbors[1]}
				<a href="/titles/{neigbors[1]}">Next</a>
			{/if}
		</div>
	</div>
	<div class="content">
		{#key $page.params.name}
			<Reveal mdFile={decodedLocation} />
		{/key}
	</div>
</div>

<style>
	.section {
		width: 100vw;
		height: 100vh;
		display: flex;
		flex-direction: column;
	}
	.section .navbar h4 {
		color: var(--primary800);
	}

	.section .content {
		width: 100%;
		flex-grow: 1;
	}

	.section .navbar {
		width: 100%;
		height: 80px;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding-inline: 5%;
	}

	.section .navbar > a {
		font-size: var(--h3);
	}
	.section .navbar > div > a {
		font-size: var(--h4);
		margin-left: 10px;
		padding-inline: 6px;
		padding-block: 4px;
	}
	.section .navbar > div > a:hover {
		background-color: var(--primary100);
		color: var(--primary800);

		border-radius: 8px;
	}

	@media screen and (width <768px) {
		.section .navbar h4 {
			display: none;
		}
	}
</style>
