<script lang="ts">
	import type { PageServerData } from './$types'
	import Posts from '$lib/shared/ui/posts.svelte'
	import Transition from '$lib/shared/transition/index.svelte'
	import { browser } from '$app/environment'
	import type { ObserverEventDetails, Options } from 'svelte-inview';
	import { onMount } from "svelte";
	import { inview } from 'svelte-inview';
	import { windowWidth, windowHeight, colorTheme } from '$lib/stores/mychart';
	import {
		siteDescription,
		siteImage,
		siteName,
		siteTitle,
		siteUrl,
		twitter,
		twitterHandle,
	} from '$lib/api/config'
	export let data: PageServerData
	
	if (browser) {
		colorTheme.set(localStorage.theme)
	}

	let isInView1 : any;
	let isInView2 : any;
	let isInView3 : any;
	let isInView4 : any;
	let resetObserver : any;

	const resetInView = () => {
        isInView1 = undefined;
		isInView2 = undefined;
		isInView3 = undefined;
		isInView4 = undefined;

	
		

		
	};

    onMount(() => {
        resetInView();
		onResize();


    });

	

	const options: Options = {
    rootMargin: '0px',
    unobserveOnEnter: true,
	};

	
	const handleChange1 = ({ detail }: CustomEvent<ObserverEventDetails>) =>
    (isInView1 = detail.inView);
	const handleChange2 = ({ detail }: CustomEvent<ObserverEventDetails>) =>
    (isInView2 = detail.inView);
	const handleChange3 = ({ detail }: CustomEvent<ObserverEventDetails>) =>
    (isInView3 = detail.inView);
	const handleChange4 = ({ detail }: CustomEvent<ObserverEventDetails>) =>
    (isInView4 = detail.inView);

	const onResize = () => {
        $windowWidth = window.innerWidth;
        $windowHeight = Math.min(window.innerHeight,700);
        $colorTheme = localStorage.theme;
	
	};

	
</script>

<svelte:window
  on:load={onResize}
  on:resize={onResize}
  />

<svelte:head>
	<title>{siteTitle}</title>
	<meta
    property="og:image"
    content="https://balance-social-image.vercel.app/api/og?title=Cardano Blockchain Analytics"
  	/>

	<meta content={siteDescription} name="description" />

	<meta content={siteTitle} property="og:title" />
	<meta content={siteUrl} property="og:url" />
	<meta content={siteDescription} property="og:description" />
	<meta content={siteName} property="og:site_name" />

	<meta content={twitterHandle} name="twitter:creator" />
	<meta content="summary_large_image" name="twitter:card" />
	<meta content={siteTitle} name="twitter:title" />
	<meta content={siteDescription} name="twitter:description" />
	<meta content={siteImage} name="twitter:image" />
</svelte:head>



<main>

	<section class="image-section">
		<div class="image-main">
			<img src="/images/perchlabs_main_v8.png" alt="mainImage">
		</div>
	</section>

	<section class="outline-section">
		<div class="outline-top-divider" />
		<div class="outline-text">
			<p>Our mission is to provide the Cardano Community with accurate, insightful decentralized network data analysis to make informed decisions and maximize success. We strive to provide exceptional curated on-chain analysis and data visualization for Cardano, and become the defacto gold standard for years to come.</p>
		</div>
		<div class="outline-bottom-divider" />
		
	</section>
	

	
	<Posts posts={data.posts.latest}>
		<h2 class="latest" slot="title">Latest Projects</h2>
		<a slot="see-more" href="/articles">
			<span>See more projects</span>
			<!-- <ArrowNarrowRightIcon width="24" height="24" aria-hidden="true" /> -->
		</a>
	</Posts>
	

	
	

</main>

<style>

	.image-section {
		display: grid;
		grid-template-columns: repeat(1, [column-start] 1fr);
		margin-top: var(--spacing-95);
			
	}

	.outline-section {
		display: grid;
		grid-template-columns: repeat(11, [column-start] 1fr);
		column-gap: var(--spacing-8);
		margin-top: var(--spacing-75);
	}
	
	.latest {
		margin-top: var(--spacing-95);
		font-family: var(--font-Doppio);
	}
	

	.image-main {
		display: flex;
        align-items: center;
        justify-content: center;
		grid-column: column-start 1 / span 1;
		
	}

	.outline-text {
		grid-column: column-start 1 / span 11;
		margin: var(--spacing-16);
		text-align: justify;
		
		font-family: var(--font-Doppio);
		font-size: 15px;
			
	}

	.outline-top-divider {
		grid-column: column-start 1 / span 11;
		border-bottom: 3px solid var(--clr-secondary);
		margin: 0;
	}

	.outline-bottom-divider {
		grid-column: column-start 1 / span 11;
		border-top: 3px solid var(--clr-secondary);
		margin: 0;
	}

	@media (min-width: 760px) {
		.image-section {
			display: grid;
			grid-template-columns: repeat(1, [column-start] 1fr);
			margin-top: var(--spacing-128);
		
		}

		

		.outline-section {
			display: grid;
			grid-template-columns: repeat(11, [column-start] 1fr);
			column-gap: var(--spacing-8);
			margin-top: var(--spacing-95);
		}

		.outline-top-divider {
			grid-column: column-start 1 / span 11;
			border-bottom: 3px solid var(--clr-secondary);
			margin: 0;
		}

		.outline-bottom-divider {
			grid-column: column-start 1 / span 11;
			border-top: 3px solid var(--clr-secondary);
			margin: 0;
		}

		.outline-text {
			grid-column: column-start 1 / span 11;
			margin: var(--spacing-16);
			text-align: justify;
			font-family: var(--font-Doppio);
			font-size: 16px;
			
		}
		
	}


	@media (min-width: 860px) {
		.image-section {
			display: grid;
			grid-template-columns: repeat(1, [column-start] 1fr);
			margin-top: var(--spacing-128);
			
		}

		
		.outline-section {
			display: grid;
			grid-template-columns: repeat(11, [column-start] 1fr);
			column-gap: var(--spacing-8);
			margin-top: var(--spacing-105);
		}

		.outline-top-divider {
			grid-column: column-start 1 / span 11;
			border-bottom: 3px solid var(--clr-secondary);
			margin: 0;
		}

		.outline-bottom-divider {
			grid-column: column-start 1 / span 11;
			border-top: 3px solid var(--clr-secondary);
			margin: 0;
		}

		.outline-text {
			grid-column: column-start 1 / span 11;
			margin: var(--spacing-24);
			text-align: justify;
			font-family: var(--font-Doppio);
			font-size: 18px;
			
		}

	}

	

	/* @media (max-width: 760px) {
		.image-section {
			display: grid;
			grid-template-columns: repeat(1, [column-start] 1fr);
			margin-top: var(--spacing-75);
		
		}

		.image-main {
			display: flex;
        	align-items: center;
        	justify-content: center;
			grid-column: column-start 1 / span 1;
			min-height: 300px;
		}

		.outline-section {
			display: grid;
			grid-template-columns: repeat(11, [column-start] 1fr);
			column-gap: var(--spacing-8);
			margin-top: var(--spacing-52);
		}

		.outline-top-divider {
			grid-column: column-start 1 / span 11;
			border-bottom: 3px solid var(--clr-secondary);
			margin: 0;
		}

		.outline-bottom-divider {
			grid-column: column-start 1 / span 11;
			border-top: 3px solid var(--clr-secondary);
			margin: 0;
		}

		.outline-text {
			grid-column: column-start 1 / span 11;
			margin: var(--spacing-24);
			text-align: justify;
			font-family: var(--font-Doppio);
			font-size: 16px;
			
		}
		
	} */

	

	
</style>


