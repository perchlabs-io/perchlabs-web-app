<script lang="ts">
	import MenuCategories from './menuCategories.svelte'
	import ThemeToggle from './themeToggle.svelte'
	import { siteName } from '$lib/api/config'
	import { colorTheme } from '$lib/stores/mychart';
	

	let previousY: number
	let currentY: number
	let clientHeight: number

	$: curTheme = {colorTheme};

	const deriveDirection = (y: number) => {
		const direction = !previousY || previousY < y ? 'down' : 'up'
		previousY = y

		return direction
	}

	$: scrollDirection = deriveDirection(currentY)
	$: offscreen = scrollDirection === 'down' && currentY > clientHeight * 4

	
</script>

<section 
	class="hero"
	class:motion-safe:-translate-y-full={offscreen}
>
<header>

	
	<div class="logo">
		<img class="image" src="/images/perchlabs_icon_v2.png" ><a class="title"  href="/">{siteName}</a>
	</div>

	<nav>
		
		
		<ThemeToggle />
		<!-- <MenuCategories /> -->
		
	</nav>
	
</header>
</section>

<style>
	header {
		position: sticky;
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		align-items: center;
		align-self: start;
		
	}
	
	.logo {
		grid-column: 1 / 1;
		display: flex;
		margin-right: auto;
		width: 350px;
		height: 40px;
		padding-left: 15px;	
		transition: all 0.3s ease-out;
	}
	.logo a::before {
		content: none;
		
	}
	
	.title {
		font-size: var(--font-35);
		font-family: var(--font-Quantico);
		padding-left: 25px;
		align-content: center;
		
		
	}
	
	.title:hover {
		color: var(--clr-txt);
		
	}

	.hero {
		position: sticky;
		top: 0; 
		margin-top: var(--spacing-16);
		padding: var(--spacing-12);
		z-index: 99;
		border-top: 1px solid var(--clr-menu-border);
		border-left: 1px solid var(--clr-menu-border);
		backdrop-filter: blur(4px);
		box-shadow: var(--shadow-sm);
	}

	.hero::before {
		content: "";
		background: var(--ba-header-bg);
		background-size: cover;
		position: absolute;
		top: 0px;
		right: 0px;
		bottom: 0px;
		left: 0px;
		opacity: 0.5;
	}
	
	nav {
		grid-column: 3 / 3;
		display: flex;
		gap: var(--spacing-16);
		margin-left: auto;
		padding-right: 15px;
		
		
		
	}
	nav :global(svg) {
		cursor: pointer;
	}

	@media (max-width: 650px) {
		.logo {
		grid-column: 1 / 1;
		display: flex;
		margin-right: auto;
		width: 300px;
		height: 35px;
		}

		.title {
		font-size: var(--font-22);
		padding-left: 19px;
		padding-top: 3.25px;
		
		
		}
		nav {
		grid-column: 3 / 3;
		display: flex;
		gap: var(--spacing-10);
		padding-right: 10px;
		
		
	}
	}

</style>