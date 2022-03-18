<script>
	import { onMount } from 'svelte';

	onMount(() => {
		M.Collapsible.init(document.querySelectorAll('.collapsible'), {});
	});
</script>

<h3>Watchlist</h3>

<div class="container">
	<div class="table-holder blue-grey darken-4">
		<table>
			<thead>
				<tr>
					<th>Name</th>

					<th class="align-right">Item Price</th>
				</tr>
			</thead>

			<tbody>
				<tr>
					<td>Alvin</td>
					<td class="align-right">$0.87</td>
				</tr>
				<tr>
					<td>Alan</td>
					<td class="align-right">$3.76</td>
				</tr>
				<tr>
					<td>Jonathan</td>
					<td class="align-right">$7.00</td>
				</tr>
			</tbody>
		</table>
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
		padding: 10px 30px;
		font-size: 20px;
		border-top: 1px solid rgba(255, 255, 255, 0.493) !important;
	}
	th {
		padding: 8px 30px;
		font-size: 12px;
		color: #f4f4f4ab;
	}
	.align-right {
		text-align: right;
	}
</style>
