<script>
	import { tickers } from '../../stores/rightNav';
	import Grid from './_grid.svelte';
	import RightSideNav from '$lib/components/RightSideNav.svelte';
	import LeftSideNav from '$lib/components/LeftSideNav.svelte';
	import MainLayout from '$lib/components/MainLayout.svelte';

	console.log($tickers);
</script>

<Grid>
	<div slot="main-layout"><MainLayout /></div>
	<div slot="left-up-nav"><LeftSideNav /></div>
</Grid>
