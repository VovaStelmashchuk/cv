<!-- eslint-disable svelte/no-navigation-without-resolve -->
<script lang="ts">
	import BentoCard from '$lib/components/BentoCard.svelte';
	import {
		personalInfo,
		socialLinks,
		experience,
		projects,
		articles,
		contributions
	} from '$lib/data';
	import Icon from '@iconify/svelte';
</script>

<svelte:head>
	<title>{personalInfo.name} | {personalInfo.title}</title>
	<meta name="description" content={personalInfo.bio} />
</svelte:head>

<!-- Minimal background gradient to give it a fresh look -->
<div
	class="fixed inset-0 z-[-1] bg-gradient-to-br from-background-primary via-[#eef2f6] to-[#e6e9f0]"
></div>

<main class="min-h-screen p-4 font-display text-label-primary md:p-8 lg:p-12">
	<div class="mx-auto max-w-6xl space-y-8">
		<!-- Header / Intro Banner -->
		<header
			class="flex flex-col items-start justify-between gap-6 pb-4 md:flex-row md:items-center"
		>
			<div>
				<h1 class="mb-2 text-4xl font-extrabold tracking-tight opacity-90 md:text-5xl">
					{personalInfo.name}
				</h1>
				<p class="text-xl font-medium text-label-secondary">{personalInfo.title}</p>
			</div>
			<div
				class="bg-white/50 border-white/50 hover:bg-white/70 flex items-center gap-2 rounded-full border px-5 py-2.5 text-label-secondary shadow-sm backdrop-blur-xl transition-all hover:-translate-y-0.5 hover:shadow-md"
			>
				<Icon icon="mdi:map-marker" class="text-[18px]" />
				<span class="font-medium tracking-wide">{personalInfo.location}</span>
			</div>
		</header>

		<!-- Bento Grid -->
		<div
			class="grid auto-rows-[minmax(120px,auto)] grid-cols-1 gap-4 md:grid-cols-4 md:gap-6 lg:grid-cols-6"
		>
			<!-- Profile Section -->
			<BentoCard class="row-span-2 md:col-span-4 lg:col-span-3 lg:row-span-4">
				<div class="flex h-full flex-col justify-end">
					<div class="mb-6">
						<img
							src="/avatar.png"
							alt={personalInfo.name}
							class="border-white/60 h-24 w-24 rounded-full border-4 object-cover shadow-md sm:h-32 sm:w-32"
						/>
					</div>
					<h1 class="mb-2 text-4xl leading-tight font-extrabold tracking-tight">About Me</h1>
					<p class="text-lg leading-relaxed text-label-secondary">
						{personalInfo.bio}
					</p>
				</div>
			</BentoCard>

			<!-- Social Links -->
			{#each socialLinks as link (link.name)}
				<BentoCard
					href={link.url}
					class="group flex items-center justify-start md:col-span-2 lg:col-span-2"
				>
					<div class="flex items-center gap-4">
						<div
							class="bg-white/50 group-hover:bg-white/80 rounded-2xl p-3 shadow-sm transition-transform group-hover:scale-110"
						>
							<Icon icon={link.icon} class="text-[28px] text-accent-secondary" />
						</div>
						<div>
							<div class="text-lg font-bold opacity-90">{link.name}</div>
							<div class="text-sm font-medium text-label-tertiary">{link.username}</div>
						</div>
					</div>
				</BentoCard>
			{/each}

			<!-- Experience Timeline -->
			<BentoCard title="Experience" class="row-span-3 md:col-span-4 lg:col-span-3">
				<div class="custom-scrollbar flex-grow space-y-6 overflow-y-auto pr-2">
					{#each experience as job, i (job.company)}
						<div class="relative ml-4 pl-6 {i !== experience.length - 1 ? 'pb-6' : ''}">
							<div
								class="bg-white/90 absolute top-0 -left-3.5 z-10 flex items-center justify-center rounded-full border border-separator-primary p-1.5 shadow-sm backdrop-blur-sm transition-transform hover:scale-110"
							>
								<Icon icon={job.icon} class="text-[16px] text-accent-secondary" />
							</div>
							<div class="mb-2 text-lg leading-none font-bold opacity-90">{job.role}</div>
							<div class="mb-3 flex flex-wrap items-center gap-2 font-medium text-label-secondary">
								{job.company}
								<span
									class="rounded-full border border-separator-secondary bg-fill-tertiary px-2.5 py-1 text-xs font-semibold"
									>{job.period}</span
								>
							</div>
							<p class="text-sm leading-relaxed text-label-tertiary">
								{job.description}
							</p>
						</div>
					{/each}
				</div>
			</BentoCard>

			<!-- Projects & Open Source -->
			<BentoCard title="Projects & Open Source" class="row-span-3 md:col-span-4 lg:col-span-3">
				<div class="grid h-full grid-cols-1 gap-4 sm:grid-cols-2">
					{#each projects as project (project.name)}
						<!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
						<a
							href={project.link}
							target={project.link === '#' ? '_self' : '_blank'}
							rel="noopener noreferrer"
							class="group border-white/50 bg-white/40 hover:bg-white/70 flex h-full flex-col rounded-2xl border p-4 shadow-sm backdrop-blur-sm transition-all duration-300 hover:-translate-y-1 hover:shadow-md"
						>
							<div class="mb-3 flex items-start justify-between">
								<div
									class="bg-white/60 rounded-xl p-2.5 shadow-sm transition-transform group-hover:scale-105"
								>
									<Icon icon={project.icon} class="text-[20px] text-accent-secondary" />
								</div>
							</div>
							<h4
								class="mb-1 text-lg font-bold opacity-90 transition-colors group-hover:text-accent-primary"
							>
								{project.name}
							</h4>
							<p class="line-clamp-3 grow leading-relaxed text-label-tertiary">
								{project.description}
							</p>
						</a>
					{/each}
				</div>
				{#if contributions && contributions.length > 0}
					<div class="mt-6 border-t border-separator-secondary pt-4">
						<h4 class="mb-3 text-sm font-bold tracking-wide text-label-secondary uppercase">
							Open Source Contributions
						</h4>
						<div class="flex flex-wrap gap-2">
							{#each contributions as item (item.name)}
								<!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
								<a
									href={item.link}
									target="_blank"
									rel="noopener noreferrer"
									class="hover:bg-white/60 rounded-full border border-separator-secondary bg-fill-secondary px-3 py-1.5 text-sm font-medium text-label-secondary shadow-sm transition-colors hover:-translate-y-0.5 hover:text-accent-primary hover:shadow-md"
								>
									{item.name}
								</a>
							{/each}
						</div>
					</div>
				{/if}
			</BentoCard>

			<!-- Writing & Thoughts -->
			<BentoCard title="Writing & Thoughts" class="md:col-span-4 lg:col-span-6">
				<div class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3">
					{#each articles as article (article.title)}
						<!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
						<a
							href={article.link}
							target="_blank"
							rel="noopener noreferrer"
							class="group border-white/50 bg-white/40 hover:bg-white/70 flex flex-col rounded-2xl border p-5 shadow-sm backdrop-blur-sm transition-all duration-300 hover:-translate-y-1 hover:shadow-md"
						>
							<div class="mb-4 flex items-center gap-4">
								<div
									class="bg-white/60 rounded-xl p-3 shadow-sm transition-transform group-hover:scale-110"
								>
									<Icon icon={article.icon} class="text-[24px] text-accent-secondary" />
								</div>
								<div
									class="line-clamp-2 text-lg leading-tight font-bold opacity-90 transition-colors group-hover:text-accent-primary"
								>
									{article.title}
								</div>
							</div>
							<p class="line-clamp-2 flex-grow leading-relaxed text-label-secondary">
								{article.description}
							</p>
						</a>
					{/each}
				</div>
			</BentoCard>
		</div>
	</div>
</main>

<style>
	/* Subtle custom scrollbar for experience section */
	.custom-scrollbar::-webkit-scrollbar {
		width: 4px;
	}
	.custom-scrollbar::-webkit-scrollbar-track {
		background: transparent;
	}
	.custom-scrollbar::-webkit-scrollbar-thumb {
		background: var(--color-separator-primary, rgba(0, 11, 33, 0.15));
		border-radius: 4px;
	}
	.custom-scrollbar:hover::-webkit-scrollbar-thumb {
		background: var(--color-separator-secondary, rgba(0, 11, 33, 0.25));
	}
</style>
