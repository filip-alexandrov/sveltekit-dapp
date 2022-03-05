<script>
	import { onMount } from 'svelte';

	let clickedOption = '';
	let options = [
		'Indices',
		'Cryptocurrency',
		'Shares',
		'Commodities',
		'Bonds and Rates',
		'ETFs',
		'Options'
	];

	/* 	onMount(() => {
		let options = {};
		let elems = document.querySelectorAll('.modal');
		let instances = M.Modal.init(elems, options);
		instances[0].open();
	}); */
</script>

<table class="highlight">
	<thead>
		<tr>
			<th>MARKETS</th>
		</tr>
	</thead>

	<tbody>
		{#each options as option}
			<tr>
				<td
					on:click={() => {
						if (clickedOption === option) {
							clickedOption = '';
						} else {
							clickedOption = option;
						}
					}}
					class={clickedOption === option ? 'clicked' : ''}>{option}</td
				>
			</tr>
		{/each}
	</tbody>
</table>
<hr />

<style lang="scss">
	table,
	th,
	td {
		font-size: max(13px, 1.5vh);
		font-weight: 500;
		user-select: none;
		border: none;
		cursor: pointer;

		thead tr th {
			cursor: default;
			font-size: max(13px, 1.5vh);
			font-family: 'Roboto Mono', monospace;
			font-weight: 300;
		}
	}

	table {
		width: 100%;
		display: table;
		border-collapse: collapse;
		border-spacing: 0;
	}
	hr {
		border-bottom: 2px solid #b5bdbe;
		border-radius: 0.5;
		border-top: none;
		width: 80%;
	}

	table.highlight > tbody > tr {
		-webkit-transition: background-color 0.25s ease;
		transition: background-color 0.25s ease;
	}

	table.highlight > tbody > tr:hover {
		background-color: #eaf1f2;
	}

	td,
	th {
		padding: 0.5vh;
		display: table-cell;
		text-align: left;
		vertical-align: middle;
	}
	.clicked {
		-webkit-transition: background-color 0.25s ease;
		transition: background-color 0.25s ease;
		background-color: #ccd5d6;
		border-left: 5px solid rgb(226, 1, 1);
		transition: border ease-in-out 0.1s;
	}
</style>
