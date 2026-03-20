<!-- eslint-disable svelte/no-navigation-without-resolve -->
<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		title?: string;
		class?: string;
		href?: string;
		children?: Snippet;
	}

	let { title = '', class: className = '', href = '', children }: Props = $props();

	// Very premium Apple-like glassmorphism aesthetic for light mode (since the project layout is light by default)
	const baseClasses =
		'relative overflow-hidden rounded-3xl bg-white/70 backdrop-blur-2xl border border-white/60 shadow-[0_8px_30px_rgb(0,0,0,0.04)] transition-all duration-300 hover:bg-white/90 hover:shadow-[0_8px_30px_rgb(0,0,0,0.08)] hover:-translate-y-1 hover:scale-[1.01] flex flex-col p-6 text-label-primary';
	const classes = $derived(`${baseClasses} ${className}`);
</script>

{#if href}
	<!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
	<a
		{href}
		target={href.startsWith('#') ? '_self' : '_blank'}
		rel="noopener noreferrer"
		class={classes}
	>
		{#if title}
			<h3 class="mb-4 font-display text-xl font-bold opacity-90">{title}</h3>
		{/if}
		{#if children}
			<div class="flex flex-grow flex-col">
				{@render children()}
			</div>
		{/if}
	</a>
{:else}
	<div class={classes}>
		{#if title}
			<h3 class="mb-4 font-display text-xl font-bold opacity-90">{title}</h3>
		{/if}
		{#if children}
			<div class="flex flex-grow flex-col">
				{@render children()}
			</div>
		{/if}
	</div>
{/if}
