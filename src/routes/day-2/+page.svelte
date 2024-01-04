<script lang="ts">
	import Cookie from './Cookie.svelte'
	import { fly } from 'svelte/transition'

	let count = 0

	const increment = () => {
		count += 1
	}

	const reset = () => {
		count = 0
	}
</script>

<div class="flex h-full w-full flex-col items-center justify-center">
	{#key count}
		<Cookie on:click={increment} />
	{/key}
	<div class="h-16 w-16">
		{#key count}
			<div
				in:fly={{ y: 50, duration: 100 }}
				out:fly={{ y: -50, duration: 100 }}
				class="select-none text-center text-3xl"
			>
				{count}
			</div>
		{/key}
	</div>
	<button class="mt-10 select-none text-2xl" on:click={reset}>reset</button>
</div>
