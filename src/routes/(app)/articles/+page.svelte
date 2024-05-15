<script lang="ts">
	import Heading from '$lib/shared/ui/heading.svelte'
	import Posts from '$lib/shared/ui/posts.svelte'
	import type { PageServerData } from './$types'
	export let data: PageServerData
</script>

<svelte:head>
	<title>Projects</title>
	<meta content="List of {data.posts.length} articles." name="description" />
	<meta
    property="og:image"
    content="https://balance-social-image.vercel.app/api/og?title=Projects"
  	/>
</svelte:head>

<Heading>Projects</Heading>

<Posts posts={data.posts}>
	<div class="container" slot="title">
		<h3>Archive</h3>
		<div class="count">
			<span class="results">{data.posts.length}</span> results
		</div>
	</div>
</Posts>

<style>
	.container {
		display: flex;
		justify-content: space-between;
	}
	.results {
		font-weight: 700;
	}
	.count {
		display: flex;
		align-items: end;
		gap: var(--spacing-10);
	}
</style>