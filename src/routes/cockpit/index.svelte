<script>
	import { tickers } from '../../stores/rightNav';
	import Grid from './_grid.svelte';
	import RightSideNav from '$lib/components/RightSideNav.svelte';
	import LeftSideNav from '$lib/components/LeftSideNav.svelte';
	import MainLayout from '$lib/components/MainLayout.svelte';
	import { fly, slide } from 'svelte/transition';
	import { linear } from 'svelte/easing';
	import Viewport from 'svelte-viewport-info';
	import MainLayout2 from '$lib/components/MainLayout2.svelte';

	let screenWidth = Viewport.Width;
	let leftExpandedMenu = screenWidth * 0.4;

	let leftNavClickedOption = '';
	let tickerClicked = '';

	function handleClickedOption(event) {
		// will be '' on second click
		leftNavClickedOption = event.detail.clickedOption;
		tickerClicked = '';
	}

	function handleTickerClicked(event) {
		tickerClicked = event.detail.tickerClicked;
	}
</script>

<Grid>
	<div class="under-leftmenu" slot="main-layout">
		{#if leftNavClickedOption != ''}
			<div
				style="display: inline-block;"
				in:fly={{ x: -leftExpandedMenu, duration: 150, opacity: 1, easing: linear }}
			>
				<MainLayout {leftNavClickedOption} on:clicked-ticker={handleTickerClicked} />
			</div>
		{/if}

		{#if tickerClicked != ''}
			<MainLayout2 {tickerClicked} />
		{/if}
	</div>
	<div class="above-expanded" slot="left-up-nav">
		<LeftSideNav on:clicked-option={handleClickedOption} />
	</div>
</Grid>
