<script>
	import { categories, github, matrix, twitter, youtube } from '$lib/api/config'
</script>

<footer>
	<div class="categories">
		<p>Category</p>
		<ul>
			{#each Object.entries(categories) as [slug, category]}
				<li>
					<a href="/categories/{slug}">{category}</a>
				</li>
			{/each}
		</ul>
	</div>

	<div class="follow">
		<p>Follow</p>
		<ul>
			<li><a href={twitter} target="_blank" rel="noreferrer">Twitter</a></li>
			<li><a href={matrix} target="_blank" rel="noreferrer">Matrix</a></li>
		</ul>
	</div>

	<div class="info">
		<p>Info</p>
		<ul>
			<li><a href="/about">About</a></li>
			<!-- <li><a href="/faq">FAQ</a></li> -->
			
		</ul>
	</div>

	

	<figure>
		
		
	</figure>
</footer>

<style>
	footer {
		display: grid;
		grid-template-columns: repeat(12, [column-start] 1fr);
		column-gap: var(--spacing-24);
		margin-top: var(--spacing-302);
		padding: var(--spacing-32);
		background-color: var(--ba-clr-footer-bg);
		border-top: 1px solid var(--clr-menu-border);
		border-left: 1px solid var(--clr-menu-border);
		
	}
	footer > * {
		grid-column: column-start 1 / span 11;
	}
	footer p {
		font-size: var(--font-20);
		font-weight: 700;
		padding-bottom: var(--spacing-8);
		
	}
	footer ul {
		width: max-content;
		display: grid;
		grid-template-rows: repeat(5, 1fr);
		grid-auto-flow: column;
		column-gap: var(--spacing-32);
		row-gap: var(--spacing-12);
		margin-top: var(--spacing-16);
		list-style-type: none;
		margin: 0;
  		padding: 0;
	}
	footer li a {
		font-weight: inherit;
		color: var(--clr-footer-txt);
	}
	footer li a:hover {
		color: var(--clr-secondary);
	}
	
	

	
	@media (min-width: 860px) {
		footer figure {
			grid-area: 1 / col8-start / last-line / 8;
		}
		footer .categories {
			grid-column: column-start 1 / span 3;
		}
		footer .follow {
			grid-column: column-start 4 / span 3;
		}
		
		footer .info {
			grid-column: column-start 1 / span 3;
		}
		
	}
	@media (min-width: 1240px) {
		footer ul {
			width: auto;
			column-gap: 0;
		}
	}
	@media (max-width: 650px) {
		footer li a {
			font-size: var(--font-14);
			font-weight: inherit;
			color: var(--clr-footer-txt);
		}
		footer p {
			font-weight: 700;
			font-size: var(--font-18);
		}
		
	}
</style>