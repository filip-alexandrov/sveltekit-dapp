<script>
	import { createEventDispatcher } from 'svelte';
	import MainLayout2 from './MainLayout2.svelte';

	export let leftNavClickedOption;

	let clickedTicker = '';
	let tickers = [
		{
			name: 'Germany 40',
			sellPrice: '13550.3',
			buyPrice: '13552.3 ',
			change: '111.5',
			percentChange: '0.83'
		},
		{
			name: 'US Tech 100',
			sellPrice: '13580.6 ',
			buyPrice: '13581.6 ',
			change: '-159.3',
			percentChange: '-1.16'
		},
		{
			name: 'Germany 40',
			sellPrice: '13550.3',
			buyPrice: '13552.3 ',
			change: '111.5',
			percentChange: '0.83'
		},
		{
			name: 'Germany 40',
			sellPrice: '13550.3',
			buyPrice: '13552.3 ',
			change: '111.5',
			percentChange: '0.83'
		}
	];
	const dispatch = createEventDispatcher();
	function openModal(tickerClicked) {
		dispatch('clicked-ticker', { tickerClicked });
	}
</script>

<div>
	<div class="modal">
		<div class="title">
			{leftNavClickedOption}
		</div>
		<div class="info-container">
			<div class="table-holder">
				<table class="highlight">
					<thead>
						<tr class="labels">
							<th>INSTRUMENT</th>
							<th class="align-right">SELL</th>
							<th class="align-right">BUY</th>
							<th class="align-right">CHANGE</th>
							<th class="align-right">%CHANGE</th>
						</tr>
					</thead>
					<tbody>
						{#each tickers as ticker}
							<tr
								on:click={() => {
									if (clickedTicker === ticker.name) {
										clickedTicker = '';
									} else {
										clickedTicker = ticker.name;
									}
									openModal(clickedTicker);
								}}
								class="ticker-data"
							>
								<td class="weight-500  {clickedTicker === ticker.name ? 'clicked' : ''}"
									>{ticker.name}</td
								>
								<td class="align-right">{ticker.sellPrice}</td>
								<td class="align-right">{ticker.buyPrice}</td>
								<td
									class="align-right {parseFloat(ticker.change) > 0
										? 'positive-change'
										: 'negative-change'}">{ticker.change}</td
								>
								<td
									class="align-right {parseFloat(ticker.percentChange) > 0
										? 'positive-change'
										: 'negative-change'}">{ticker.percentChange}</td
								>
							</tr>
						{/each}
					</tbody>
				</table>
			</div>
		</div>
	</div>
</div>

<style lang="scss">
	.table-holder {
		margin: 2% 0%;
		padding-left: 3%;
		padding-right: 3%;
	}
	.modal {
		background-color: #f0f5f6;
		width: 35vw;

		color: #11203e;
		height: 96.5vh;
	}
	.info-container {
		width: 95%;
		height: 90%;
		background-color: #fff;
		position: relative;
		top: 3%;
		left: 2%;

		box-shadow: 0.1vw 0.2vh 0.8vh 0.1vh rgba(100, 100, 111, 0.2);
		border-radius: 0.4%;
		overflow: auto;
	}
	.title {
		position: relative;
		left: 6%;
		top: 2vh;
		font-size: max(2vw, 20px);
		font-weight: 500;
	}

	.positive-change {
		color: rgb(0, 135, 224);
	}

	table,
	th,
	td {
		.weight-500 {
			font-weight: 500;
			cursor: pointer;
		}
		.align-right {
			text-align: right;
		}
		width: 100%;

		font-size: max(13px, 1.5vh);
		font-weight: 400;
		user-select: none;
		border: none;
		cursor: default;

		thead tr th {
			cursor: default;
			font-size: max(13px, 1.5vh);
			font-family: 'Roboto Mono', monospace;
			font-weight: 300;
			white-space: nowrap;
			color: #868686;
		}
	}

	table {
		width: 100%;
		display: block;
		border-collapse: collapse;
		border-spacing: 0;
	}

	.ticker-data {
		border-bottom: 1px solid #ccd5d68a;
	}

	table.highlight > tbody > tr {
		-webkit-transition: background-color 0.25s ease;
		transition: background-color 0.25s ease;
	}

	table.highlight > tbody > tr:hover {
		background-color: #dce6e7;
	}

	td,
	th {
		padding: 0.5vh;
		display: table-cell;
		text-align: left;
		vertical-align: middle;
	}
	.clicked {
		~ td {
			-webkit-transition: background-color 0.25s ease;
			transition: background-color 0.25s ease;
			background-color: #ccd5d6;
		}
		-webkit-transition: background-color 0.25s ease;
		transition: background-color 0.25s ease;
		background-color: #ccd5d6;
		border-left: 5px solid rgb(226, 1, 1);
		transition: border ease-in-out 0.1s;
	}
	.negative-change {
		color: rgb(226, 1, 1);
	}
</style>
