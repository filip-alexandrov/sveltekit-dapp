<script context="module">
	// module runs before component is created
	export const load = ({ url, params }) => {
		const ticker = params.ticker;
		return {
			props: {
				ticker
			}
		};
	};
</script>

<script>
	import { onMount } from 'svelte/internal';
	export let ticker;

	let modalInstance;
	onMount(() => {
		M.Tabs.init(document.querySelectorAll('.tabs'), {});
		M.Sidenav.init(document.querySelectorAll('.sidenav'), {});
		modalInstance = M.Modal.init(document.querySelectorAll('.modal'), {});
	});

	let menuOptionClicked = 'Buy';
	let menuOptions = ['Buy', 'Sell'];

	function handleMenuOptionClick(option) {
		menuOptionClicked = option;
	}

	const insurancePolicies = [
		{
			direction: 'up',
			level: 120,
			price: 4,
			openInterest: 240
		},
		{
			direction: 'up',
			level: 120,
			price: 4,
			openInterest: 240
		},
		{
			direction: 'up',
			level: 120,
			price: 4,
			openInterest: 240
		}
	];
</script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css"
	/>
	<script
		src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>
	<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
</svelte:head>

<nav class="nav-extended blue-grey darken-4">
	<div class="nav-wrapper">
		<a href="/mobile" class="brand-logo center">Matterhorn</a>
		<a href="" data-target="slide-out" class="sidenav-trigger show-on-large"
			><i class="material-icons">menu</i></a
		>
	</div>
	<div class="nav-content">
		<ul class="tabs tabs-transparent">
			{#each menuOptions as option}
				<li class="tab">
					<a
						href="#{option}"
						on:click={() => handleMenuOptionClick(option)}
						class={menuOptionClicked == option ? 'active' : ''}>{option}</a
					>
				</li>
			{/each}
		</ul>
	</div>
</nav>

<ul class="sidenav" id="slide-out">
	<li><a href="sass.html">Sass</a></li>
	<li><a href="badges.html">Components</a></li>
	<li><a href="collapsible.html">JavaScript</a></li>
</ul>
<div class="container">
	<h3 class="blue-grey-text text-darken-4">{menuOptionClicked} {ticker} Insurance</h3>
</div>

<div class="container">
	<div class="table-holder blue-grey darken-4">
		<table>
			<thead>
				<tr>
					<th>Dir</th>
					<th>Level</th>
					<th>Avg. Price</th>
					<th class="align-right">Open Int.</th>
				</tr>
			</thead>

			<tbody>
				{#each insurancePolicies as policy}
					<tr
						on:click={() => {
							modalInstance[0].open();
						}}
					>
						<td>{policy.direction}</td>
						<td>${policy.level}</td>
						<td>${policy.price}</td>
						<td class="align-right">{policy.openInterest}</td>
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
	:global(body) {
		background-color: #eceff1;
	}
	.fullscreen {
		width: 100%;
		height: 100%;
	}

	.tab a {
		background-color: transparent !important;
	}
	.current-price {
		background-color: #0099ff !important;
		font-size: 18px;
		padding: 14px;
	}
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
