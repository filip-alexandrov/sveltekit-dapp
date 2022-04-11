<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	let modalInstance;
	onMount(() => {
		M.Collapsible.init(document.querySelectorAll('.collapsible'), {});
		modalInstance = M.Modal.init(document.querySelectorAll('.modal'), {});
	});

	// stock object with name and price
	const watchlistTickers = [
		{
			name: 'APPL',
			price: 110
		},
		{
			name: 'MSFT',
			price: 80
		},
		{
			name: 'TSLA',
			price: 90
		}
	];
</script>

<div class="container">
	<h3 class="blue-grey-text text-darken-4">Watchlist</h3>
	<div class="table-holder blue-grey darken-4">
		<table>
			<thead>
				<tr>
					<th>Ticker</th>

					<th class="align-right">Price</th>
				</tr>
			</thead>

			<tbody>
				{#each watchlistTickers as ticker}
					<tr
						on:click={() => {
							/* goto('/mobile/trade/' + ticker.name); */
							modalInstance[0].open();
						}}
					>
						<td>{ticker.name}</td>
						<td class="align-right">${ticker.price}</td>
					</tr>
				{/each}
			</tbody>
		</table>
	</div>
</div>

<!-- Modal Structure -->
<div id="modal1" class="modal">
	<div class="modal-content">
		<h4>AAPL Insurance</h4>

		<p>A bunch of text</p>
	</div>
	<div class="modal-footer">
		<a href="#!" class="modal-close waves-effect waves-green btn-flat">Agree</a>
	</div>
</div>

<style>
	.table-holder {
		cursor: pointer;
		background-color: aqua;
		border-radius: 16px;
		color: #f4f4f4;
		box-shadow: 0.5vw 0.5vh 2vh 1vh rgba(100, 100, 111, 0.2) !important;
	}

	td {
		padding: 10px 20px;
		font-size: 20px;
		border-top: 1px solid rgba(255, 255, 255, 0.493) !important;
	}
	th {
		padding: 8px 20px;
		font-size: 12px;
		color: #f4f4f4ab;
	}
	.align-right {
		text-align: right;
	}
</style>
