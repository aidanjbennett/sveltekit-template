<script lang="ts">
	import { page } from '$app/stores';

	function resolveErrorCode(code: number) {
		switch (code) {
			case 404:
				return {
					title: 'Page not found',
					subtitle: 'The page you are looking for does not exist.'
				};
			case 500:
				return {
					title: 'Internal server error',
					subtitle: 'Something went wrong on our end.'
				};
			default:
				return {
					title: 'Unknown error',
					subtitle: $page.error?.message || 'Something went wrong.'
				};
		}
	}

	$: error = resolveErrorCode($page.status || 500);
</script>

<head>
	<title>{error.title}</title>
	<meta name="robots" content="noindex" />
</head>

<h1 class="text-center text-3xl mt-4">Error: {$page.status}</h1>

{#if $page.status === 404}
	<p class="text-center text-3xl">The page you are looking for does not exist.</p>
	<h1 class="text-center">
		<a href="/" class="text-3xl hover:underline">Return back to safety</a>
	</h1>
{:else}
	<h2 class="text-center text-3xl">{error.title}</h2>
	<p class="text-center text-3xl">{error.subtitle}</p>
{/if}
