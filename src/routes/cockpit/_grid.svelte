<script lang="ts" context="module">
	import Device from 'svelte-device-info';
	import Viewport from 'svelte-viewport-info';
</script>

<script lang="ts">
	let devicePhone: boolean = false;
	let deviceComputer: boolean = false;
	let deviceTablet: boolean = false;
	let orientation: string = '';

	switch (true) {
		case Device.isPhone:
			devicePhone = true;
			break;
		case Device.isTablet:
			deviceTablet = true;
			break;
	}
	if (Device.isMobile == false) deviceComputer = true;

	orientation = Viewport.Orientation;
</script>

<svelte:head>
	<link rel="icon" type="image/svg" />
	<title>Cockpit | A&A Globals</title>
</svelte:head>

<svelte:body
	on:orientationchangeend={() => {
		orientation = Viewport.Orientation;
	}} />

{#if deviceComputer || deviceTablet}
	<div class="full-screen">
		<div class="grid-container">
			<div class="main-part"><slot name="main-layout">Loading...</slot></div>
			<div class="item2">1</div>
			<div class="item2">2</div>
			<div class="item3">3</div>
			<div class="item4">4</div>
			<div class="item5">5</div>
			<div class="item6">6</div>
			<div class="item6">7</div>

			<div class="left-up-nav">
				<slot name="left-up-nav">Loading...</slot>
			</div>
			<div class="item7"><slot name="right-up-nav">Loading...</slot></div>

			<div class="item7"><slot name="left-down-nav">Loading...</slot></div>
			<div class="item7"><slot name="right-down-nav">Loading...</slot></div>
		</div>
	</div>
{:else}
	<h1>Device is Phone</h1>
{/if}

<style lang="scss">
	:global(body, html) {
		height: 100%;
		width: 100%;
		margin: 0;
		font-family: 'Roboto', sans-serif;
		color: #11203e;
		overflow-y: hidden;
	}

	.grid-container {
		height: 100vh;
		display: grid;
		grid-template-columns: 7.5% auto auto auto auto auto 7.5%;
		grid-template-rows: 3.5vh 55vh auto;
		grid-gap: 0px;
		background-color: #fff;
		box-sizing: border-box;

		div {
			font-size: max(1vw, 15px);
		}
	}

	.item7 {
		align-items: flex-start !important;
		padding-left: 1px;
		text-overflow: ellipsis;
		overflow: hidden;
		white-space: nowrap;
	}

	.main-part {
		grid-area: 2 / 2 / span 2 / span 5;
	}
	.left-up-nav {
		font-size: max(1vw, 15px);
		align-items: flex-start !important;
		padding-left: 1px;
		text-overflow: ellipsis;
		overflow-x: hidden;
		white-space: nowrap;
		z-index: 1;

		&::-webkit-scrollbar {
			display: none;
		}
		-ms-overflow-style: none; /* IE and Edge */
		scrollbar-width: none; /* Firefox */

		background-color: #f0f5f6;
	}
</style>
