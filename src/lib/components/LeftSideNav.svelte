<script>
	import { createEventDispatcher } from 'svelte';

	let clickedOption = '';
	let options = [
		'Indices',
		'FX',
		'Cryptocurrency',
		'Shares',
		'Commodities',
		'Bonds and Rates',
		'ETFs',
		'Options'
	];

	let popularToday = ['S&P500', 'Dow Jones', 'Apple', 'Tesla', 'Microsoft', 'Netflix'];

	const dispatch = createEventDispatcher();
	function openModal(clickedOption) {
		dispatch('clicked-option', { clickedOption });
		console.log('clicked in nav component');
	}
</script>

<table class="highlight move-down">
	<tbody>
		<tr>
			<td
				on:click={() => {
					if (clickedOption === 'Search') {
						clickedOption = '';
					} else {
						clickedOption = 'Search';
					}
					openModal(clickedOption);
				}}
				class={clickedOption === 'Search' ? 'clicked' : ''}>Search <span class="right">🔍</span></td
			>
		</tr>
	</tbody>
</table>

<hr />

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
						openModal(clickedOption);
					}}
					class={clickedOption === option ? 'clicked' : ''}
					>{option}
				</td>
			</tr>
		{/each}
	</tbody>
</table>
<hr />

<table class="highlight">
	<thead>
		<tr>
			<th>POPULAR</th>
		</tr>
	</thead>

	<tbody>
		{#each popularToday as popularName}
			<tr>
				<td
					on:click={() => {
						if (clickedOption === popularName) {
							clickedOption = '';
						} else {
							clickedOption = popularName;
						}
						openModal(clickedOption);
					}}
					class={clickedOption === popularName ? 'clicked' : ''}
				>
					{popularName}</td
				>
			</tr>
		{/each}
	</tbody>
</table>

<style lang="scss">
	.move-down {
		margin-top: 2vh;
	}
	.right {
		float: right;
	}
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
			white-space: nowrap;
		}

		span.percent-change {
			color: green;
			float: right;
		}
	}

	table {
		width: 100%;
		display: table;
		border-collapse: collapse;
		border-spacing: 0;
	}
	hr {
		border-bottom: 1px solid #b5bdbe;
		border-radius: 0.5;
		border-top: none;
		width: 80%;
	}

	table.highlight > tbody > tr {
		-webkit-transition: background-color 0.25s ease;
		transition: background-color 0.25s ease;
	}

	table.highlight > tbody > tr:hover {
		background-color: #ccd5d6;
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
