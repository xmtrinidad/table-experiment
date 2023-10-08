<script lang="ts">
	export let player;
	let tableContainer: HTMLElement;
	const generateJSON = async () => {
		const table = tableContainer.querySelector('table');
		const tbody = table.querySelector('tbody');
		const rows = Array.from(tbody.querySelectorAll('tr'));
		const stats = rows.map((row) => {
			const columns = Array.from(row.querySelectorAll('td'));
			return {
				dur: columns[0].textContent.trim().replace('Last ', '').replace(' Games', 'G'),
				AB: +columns[1].textContent.trim(),
				R: +columns[2].textContent.trim(),
				H: +columns[3].textContent.trim(),
				HR: +columns[4].textContent.trim(),
				RBI: +columns[5].textContent.trim(),
				BB: +columns[6].textContent.trim(),
				SO: +columns[7].textContent.trim(),
				SB: +columns[8].textContent.trim(),
				AVG: parseFloat(columns[9].textContent.trim()),
				OBP: parseFloat(columns[10].textContent.trim()),
				SLG: parseFloat(columns[11].textContent.trim())
			};
		});

		const jsonData = {
			name: player.name,
			stats: stats
		};

		const jsonDataStr = JSON.stringify(jsonData, null, 2);

		try {
			await navigator.clipboard.writeText(jsonDataStr);
			// alert('JSON copied to clipboard!');
		} catch (err) {
			console.error('Failed to copy JSON: ', err);
		}
	};
</script>

<h2>{player.name}</h2>
<div bind:this={tableContainer}>
	{@html player.htmlTable}
</div>

<button on:click={generateJSON}>Convert to JSON</button>

<style>
	:global(table) {
		width: 100%;
		border-collapse: collapse;
		margin-bottom: 8px;
	}

	:global(th),
	:global(td) {
		padding: 10px;
		text-align: center;
		border: 1px solid #ddd;
	}

	:global(thead) :global(th) {
		background-color: #4caf50;
		color: white;
		font-weight: bold;
		text-transform: uppercase;
		border-top: 2px solid #4caf50;
		border-bottom: 2px solid #4caf50;
	}

	:global(tr:nth-child(even)) {
		background-color: #f2f2f2;
	}

	:global(tr:nth-child(odd)) {
		background-color: #ffffff;
	}

	:global(tr:hover) {
		background-color: #e0e0e0;
	}

	button {
		width: fit-content;
		cursor: pointer;
		padding: 4px;
	}
</style>
