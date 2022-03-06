<script>
	import { tickers } from '../../stores/rightNav';
	import Grid from './_grid.svelte';
	import RightSideNav from '$lib/components/RightSideNav.svelte';
	import LeftSideNav from '$lib/components/LeftSideNav.svelte';
	import MainLayout from '$lib/components/MainLayout.svelte';
	import { fly, slide } from 'svelte/transition';
	import { linear } from 'svelte/easing';
	import Viewport from 'svelte-viewport-info';

	let screenWidth = Viewport.Width;
	let leftExpandedMenu = screenWidth * 0.4;

	console.log($tickers);

	let leftNavClickedOption = '';
	function handleClickedOption(event) {
		if (leftNavClickedOption == event.detail.clickedOption) {
			leftNavClickedOption = '';
		} else {
			leftNavClickedOption = event.detail.clickedOption;
		}
	}
</script>

<Grid>
	<div class="under-leftmenu" slot="main-layout">
		{#if leftNavClickedOption != ''}
			<div in:fly={{ x: -leftExpandedMenu, duration: 150, opacity: 1, easing: linear }}>
				<MainLayout {leftNavClickedOption} />
			</div>
		{/if}
	</div>
	<div class="above-expanded" slot="left-up-nav">
		<LeftSideNav on:clicked-option={handleClickedOption} />
	</div>
</Grid>

<style>
</style>
