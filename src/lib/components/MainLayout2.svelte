<script>
	import { onDestroy, onMount } from 'svelte';

	import TradingViewWidget from 'svelte-tradingview-widget';

	export let tickerClicked;
	$: TWoptions = {
		symbol: tickerClicked,
		theme: 'light',
		autosize: true,
		locale: 'en',
		interval: 'D',
		allow_symbol_change: false,
		details: true
	};

	onDestroy(() => {
		console.log('destroyed');
	});

	let clickedOption = '';
	let tradingOptions = ['Deal', 'Order', 'Alert', 'Info'];

	function handleTradingClick(option) {
		if (clickedOption == option) {
			clickedOption = '';
		} else {
			clickedOption = option;
		}
	}
</script>

<div class="modal2">
	<div class="title">{tickerClicked}</div>
	<div class="info-container">
		<div class="trading-view">
			{#if TWoptions}
				<TradingViewWidget options={TWoptions} />
			{/if}
		</div>
		<div class="trading-control">
			<!-- <table class="table highlight">
				<tbody>
					{#each tradingOptions as option}
						<tr
							on:click={() => handleTradingClick(option)}
							class={clickedOption == option ? 'clicked' : ''}
						>
							<td>
								{option}
							</td>
						</tr>
					{/each}
				</tbody>
			</table> -->
			<div class="trading-selector">
				<ul>
					<li class="clicked">Deal</li>
					<li>Order</li>
					<li>Alert</li>
					<li>Info</li>
				</ul>
			</div>

			<div class="trading-window">
				<div class="btn">
					<div class="trade-type">BUY</div>
					<div class="trade-price">13580.81</div>
				</div>
				<div class="btn">
					<div class="trade-type">SELL</div>
					<div class="trade-price">13580.81</div>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	.modal2 {
		position: absolute;
		display: inline-block;
		background-color: #f0f5f6;

		width: 53vw;

		height: 96.5vh;
	}
	.title {
		position: relative;
		left: 4%;
		top: 2vh;
		font-size: max(2vw, 20px);
		font-weight: 500;
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
	.trading-view {
		height: 80%;
		width: 100%;
	}

	.trading-control {
		top: 2vh;
		position: relative;
		width: 100%;
		vertical-align: middle;
		display: flex;
		align-items: stretch;
	}

	/* 	table,
	th,
	td {
		border: none;
		vertical-align: middle;
		cursor: pointer;
		vertical-align: center;
	}

	table {
		width: 100%;
		display: table;
		border-collapse: collapse;
		border-spacing: 0;
	}
	table.highlight > tbody > tr {
		-webkit-transition: background-color 0.25s ease;
		transition: background-color 0.25s ease;
	}

	table.highlight > tbody > tr:hover {
		background-color: rgb(185, 185, 185);
	}

	td,
	th {
		padding: 1vh 1vh;
		display: table-cell;
		text-align: left;
		vertical-align: middle;
		font-weight: 500;
		font-size: 1.7vh;
		text-align: right;
	}
	.clicked {
		-webkit-transition: background-color 0.25s ease;
		transition: background-color 0.25s ease;
		background-color: #ccd5d6;
		border-left: 5px solid rgb(226, 1, 1);
		transition: border ease-in-out 0.1s;
	} */

	.trading-selector {
		width: 10%;
		height: 100%;
		margin-left: 2vw;
		display: inline-block;
	}
	ul {
		overflow: hidden;
		padding: 0;
		margin: 0;
		cursor: pointer;
		text-align: right;
	}
	li {
		list-style: none;
		font-weight: 500;
		padding: 0.7vh 0.5vw;
	}
	li:hover {
		background-color: #ccd5d6;
	}
	.clicked {
		-webkit-transition: background-color 0.25s ease;
		transition: background-color 0.25s ease;
		background-color: #ccd5d6;
		border-left: 5px solid rgb(226, 1, 1);
		transition: border ease-in-out 0.1s;
	}
	.trading-window {
		position: relative;
		display: inline-block;
		width: 80%;
		background-color: #ccd5d6;
		vertical-align: top;
	}
	.btn {
		margin-top: 1%;
		margin-left: 1%;
		height: 40%;
		width: 20%;

		background-color: #fff;
		border-radius: 4px;
		box-shadow: 0.1vw 0.2vh 0.2vh 0.05vh rgba(100, 100, 111, 0.2);

		padding-top: 3px;
		padding-left: 5px;
		padding-right: 10px;

		overflow: hidden;
	}
	.trade-type {
		font-size: 85%;
		font-weight: 500;
		position: relative;
	}
	.trade-price {
		position: relative;

		font-weight: 500;
		font-size: 120%;
	}
</style>
