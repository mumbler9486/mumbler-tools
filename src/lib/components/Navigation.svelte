<script lang="ts">
	import type { SvelteComponent } from 'svelte';
	import { Document } from 'svelte-heros-v2';

	const navGroups: NavigationGroup[] = [
		{
			label: 'Text Tools',
			icon: Document,
			items: [
				{
					label: 'CSV to JSON Editor',
					link: '/tools/text/csv-to-json',
				},
				{
					label: 'JSON List Editor',
					link: '/tools/text/json-list-editor',
				},
			],
		},
	];

	interface NavigationGroup {
		label: string;
		icon?: typeof SvelteComponent<{}>;
		items: Navigation[];
	}

	interface Navigation {
		label: string;
		link: string;
	}
</script>

<div class="drawer lg:drawer-open">
	<input id="my-drawer-3" type="checkbox" class="drawer-toggle" />
	<div class="drawer-content flex flex-col">
		<!-- Navbar -->
		<div class="navbar w-full bg-base-300">
			<div class="flex-none lg:hidden">
				<label for="my-drawer-3" aria-label="open sidebar" class="btn btn-square btn-ghost">
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						class="inline-block h-6 w-6 stroke-current"
						><path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M4 6h16M4 12h16M4 18h16"
						></path></svg
					>
				</label>
			</div>
			<div class="mx-2 flex-1 px-2"></div>
			<div class="hidden flex-none lg:block">
				<ul class="menu menu-horizontal">
					<!-- Navbar menu content here -->
					<li><a href="https://github.com/mumbler9486/mumbler-tools">Source Code</a></li>
				</ul>
			</div>
		</div>
		<slot />
	</div>
	<div class="drawer-side">
		<label for="my-drawer-3" aria-label="close sidebar" class="drawer-overlay"></label>
		<div
			data-sveltekit-preload-data=""
			class="sticky top-0 z-20 hidden items-center gap-2 bg-base-100 bg-opacity-90 px-4 py-2 shadow-sm backdrop-blur lg:flex"
		>
			<a
				href="/"
				aria-current="page"
				aria-label="Homepage"
				class="flex-0 btn btn-ghost px-2"
				data-svelte-h="svelte-nce89e"
			>
				<img class="w-8" src="/favicon.png" alt="Wrench" />
				<div class="font-title inline-flex text-lg md:text-2xl">Mumbler-Tools</div></a
			>
		</div>
		<ul class="menu w-80 p-4">
			{#each navGroups as group}
				<li>
					<details open>
						<summary>
							{#if !!group.icon}
								<svelte:component this={group.icon} />
							{/if}
							{group.label}
						</summary>
						<ul>
							{#each group.items as item}
								<li><a href={item.link}>{item.label}</a></li>
							{/each}
						</ul>
					</details>
				</li>
			{/each}
		</ul>
	</div>
</div>
