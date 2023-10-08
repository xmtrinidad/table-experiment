<script lang="ts">
	import StatsTable from '$lib/StatsTable.svelte';
	import { TEAM_1 } from '$lib/table_data/rawData';
</script>

<header>
	<h1>Stats</h1>
</header>
<div class="stats-tables">
	{#each TEAM_1 as player}
		<StatsTable {player} />
	{/each}
</div>

<style>
	header {
		background-color: #4caf50;
		color: white;
		padding: 20px;
		text-align: center;
		box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2);
	}

	header h1 {
		font-size: 36px;
		margin: 0;
		padding: 10px;
	}

	.stats-tables {
		padding: 24px;
		display: flex;
		flex-direction: column;
		gap: 24px;
	}
</style>
