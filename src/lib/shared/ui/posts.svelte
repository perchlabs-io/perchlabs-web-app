<script lang="ts">
	//import { EyeIcon } from '@rgossiaux/svelte-heroicons/outline'
	import Transition from '$lib/shared/transition/index.svelte'
	import { inview } from 'svelte-inview';
	import type { ObserverEventDetails, Options } from 'svelte-inview';
	import { views } from '$lib/stores/views'
	import type { PostType } from '$lib/types'
	import Icon from '@iconify/svelte';
	import { imagesUrl } from '$lib/api/config'
	import ErgoIcon from '$lib/icons/Ergo_Icon.svg'
	import CardanoIcon from '$lib/icons/Cardano_Icon.svg'
	export let posts: PostType[]

	let isInView : any;
	const options: Options = {
    rootMargin: '0px',
    unobserveOnEnter: true,
	};

	const handleChange = ({ detail }: CustomEvent<ObserverEventDetails>) =>
    (isInView = detail.inView);


</script>

<section>
	<slot name="title" />

	<div class="cards" use:inview="{options}" on:inview_change="{handleChange}">

		{#if isInView}
		{#each posts as post, index}
			<Transition transition={{ type: 'stagger', duration: index, delay: 400 }}>
				<a href="/{post.slug}">
					<article class="card">
						<div class="views">
							<Icon icon="ph:eye" width="1.6em" height="1.6em" />
							
							{#if $views.length > 0}
								<span>
									{$views
										.find((data) => data.slug === post.slug)
										?.views.toLocaleString() ?? 0}
								</span>
							{/if}
							
						</div>
						<span class="category">
							{#if post.category == "service"}
							<Icon icon="ic:baseline-miscellaneous-services" width="2em" height="2em" />

							{:else if post.category == "analytics"}

							{:else if post.category == "research"}

							{:else}

							{/if}	
						</span>
						<div class="details">
							<p class="title">{post.title}</p>
						
						
							<p class="description">{post.description}</p>
						</div>
						<div class="image">
							<img
								src='{imagesUrl}/{post.slug}/images/ba_svl_image_dark.png'
								alt="Test"
								style="border-radius: var(--rounded-8);"
								
							/>
						</div>
						<div class="network">
						
							{#if post.network == "ergo"}
							<ErgoIcon width="30" height="30" stroke= var(--clr-card-txt) fill= var(--clr-card-txt)/>
							{:else}
							<CardanoIcon width="33" height="33" stroke= var(--clr-card-txt) fill= var(--clr-card-txt)/>
							{/if}
						
						</div>
						<div class="status">
							{#if post.status == "in progress"}
								<Icon icon="carbon:in-progress" width="2em" height="2em" />
							{:else if post.status == "complete"}
								<Icon icon="fluent-mdl2:completed" width="2em" height="2em" />
							{:else}
								<Icon icon="material-symbols:pending-outline" width="2em" height="2em" />
							{/if}
						</div>
					</article>
				</a>
			</Transition>
		{/each}
		{/if}
	</div>

	<slot name="see-more" />
</section>

<style>
	section {
		margin-top: var(--spacing-64);
		
	}

	.cards {
		display: grid;
		gap: var(--spacing-24);
		grid-template-columns: repeat(auto-fill, minmax(282px, 1fr));
		margin-top: var(--spacing-32);

	}

	.cards a {
		display: block;
		color: inherit;
		font-weight: inherit;
		text-decoration: none;
		transition: color 0.3s ease;

	}
	.cards a::before {
		content: none;
		
	}

	.card {
		height: 600px;
		display: grid;
		grid-template-columns: repeat(3, [column-start] 1fr);
		grid-template-rows: min-content;
		padding: var(--spacing-16);
		background-image: var(--ba-clr-card-bg);
		border-top: 1px solid var(--clr-menu-border);
		border-left: 1px solid var(--clr-menu-border);
		box-shadow: var(--shadow-sm);
		transition: transform 0.2s ease-in-out, box-shadow 0.3s ease,
			outline 0.1s ease;
			
	}

	.card:hover {
		transform: scale(1.02);
		box-shadow: var(--shadow-md), 0 0 0 4px var(--clr-secondary);

	}

	.card .views {
		display: flex;
		align-items: center;
		grid-column: column-start 1 / span 1;
		gap: var(--spacing-8);
		font-family: var(--font-Doppio);
		font-size: var(--font-16);
		color: var(--clr-card-txt);

	}

	.card .category {
		display: flex;
		align-items: center;
        justify-content: end;
		grid-column: column-start 3 / span 1;
		color: var(--clr-card-txt);
		
	}

	.card .network {
		display: flex;
		grid-column: column-start 1 / span 1;
		align-items: center;
		margin-bottom: 0;
		margin-top: auto;
        
	}

	.card .image {
		grid-column: column-start 1 / span 3;
		width: 100%;
		border-radius: var(--rounded-4);
        
	}

	.card .status {
		display: flex;
		grid-column: column-start 3 / span 1;
        align-items: center;
        justify-content: end;
		color: var(--clr-card-txt);
		margin-bottom: 0;
		margin-top: auto;

	}

	.card .details {
		grid-column: column-start 1 / span 3;
		
	}

	.card .title {
		font-family: var(--font-Doppio);
		font-size: var(--font-32);
		line-height: 48px;
		margin-top: var(--spacing-8);

	}
	
	.card .description {
		margin-top: var(--spacing-16);
		font-family: var(--font-Doppio);
		color: var(--clr-card-txt);

	}

	:global([slot='see-more']) {
		width: max-content;
		display: flex;
		gap: var(--spacing-16);
		margin-top: var(--spacing-32);
		//margin-bottom: var(--spacing-105);
		
	}

	

	@media (max-width: 650px) {
		.card .title {
			font-family: var(font-sans);
			font-size: var(--font-22);
			font-weight: 700;
			line-height: 40px;
			margin-top: var(--spacing-16);

		}
		.card .views {
			display: flex;
			font-size: var(--font-16);
			align-items: center;
			gap: var(--spacing-4);
			font-weight: 500;
			color: var(--clr-card-txt);
		}
		.card .category {
			margin-right: 0;
			margin-left: auto;
			font-size: var(--font-16);
			gap: var(--spacing-4);
			font-weight: 500;
			color: var(--clr-card-txt);
		}
		.card {
			height: 525px;
			display: grid;
			grid-template-rows: min-content;
			padding: var(--spacing-16);
			background-image: var(--ba-clr-card-bg);
			border-top: 1px solid var(--clr-menu-border);
			border-left: 1px solid var(--clr-menu-border);
			box-shadow: var(--shadow-sm);
			transition: transform 0.2s ease-in-out, box-shadow 0.3s ease,
				outline 0.1s ease;
			
		}
	
	
}
</style>