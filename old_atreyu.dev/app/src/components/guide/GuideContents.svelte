<ul class='guide-toc'>
	{#each $guide_contents as section}
		<li>
			<a class='section {section.slug === $activeGuideSection ? "active": ""}' href='guide#{section.slug}'>{section.metadata.title}</a>
			{#each section.subsections as subsection}
				<a class='subsection {subsection.slug === $activeGuideSection ? "active": ""}' href='guide#{subsection.slug}'>{subsection.title}</a>
			{/each}
		</li>
	{/each}
</ul>

<style>
	.guide-toc {
		margin: 0;
		padding: 0;
	}

	.guide-toc li {
		display: block;
		margin: 0 0 2em 0;
	}

	.section {
		display: block;
		font-weight: 700;
		color: #333;
		font-size: 1.2rem;
		margin: 0 0 0.15em 0;
	}

	.subsection {
		display: block;
		font-weight: 500;
		color: #727272;
		font-size: 1em;
		margin: 0 0 0.15em 0;
	}

	.section.active, .subsection.active {
		color: rgb(20,87,138);
	}

	.section.active::before, .subsection.active::before  {
	  content: '>';
    left: -0.8em;
    position: absolute;
	}
</style>

<script>
	export default {
		data() {
			return {
				contents: []
			}
		},

		oncreate () {
			const onhashchange = () => {
				this.store.set({ activeGuideSection: window.location.hash.slice( 1 ) });
			};

			window.addEventListener( 'hashchange', onhashchange, false );
			this.on( 'destroy', () => {
				window.removeEventListener( 'hashchange', onhashchange, false );
			});

			onhashchange();
		}
	};
</script>
