<script>
	import { element, onMount } from 'svelte/internal';
	import Account from './_account.svelte';
	import Markets from './_markets.svelte';
	import Watchlist from './_watchlist.svelte';
	onMount(() => {
		M.Tabs.init(document.querySelectorAll('.tabs'), {});
		M.Sidenav.init(document.querySelectorAll('.sidenav'), {});
	});

	let menuOptionClicked = 'Watchlist';
	let menuOptions = ['Watchlist', 'Markets', 'Account'];

	function handleMenuOptionClick(option) {
		if (option == menuOptionClicked) {
			menuOptionClicked = '';
		} else {
			menuOptionClicked = option;
		}
	}
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

<div class="fullscreen blue-grey lighten-5">
	{#if menuOptionClicked == 'Watchlist'}
		<Watchlist />
	{:else if menuOptionClicked == 'Markets'}
		<Markets />
	{:else if menuOptionClicked == 'Account'}
		<Account />
	{/if}
</div>

<style>
	:global(body) {
		background-color: #eceff1;
	}
	.fullscreen {
		width: 100%;
		height: 100%;
	}
	.active {
		color: wihte !important;
	}
	.tab a {
		background-color: transparent !important;
	}
</style>
