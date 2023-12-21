<script lang="ts">
	import { onMount } from 'svelte'

	const url = `https://advent.sveltesociety.dev/data/2023/day-one.json`

	interface Child {
		name: string
		tally: number
	}

	let children: Child[]

	const getChildren = async (): Promise<Child[]> => {
		const result = await fetch(url, {
			method: 'GET'
		})

		return result.json()
	}

	let keyword: string
	let result: any = ''

	const onSearch = (keyword: string) => {
		const target = children.find((child) => child.name === keyword)
		if (target) {
			result = target.tally > 0 ? 'nice' : 'naughty'
		} else {
			result = 'Searching...'
		}
	}

	onMount(async () => {
		children = await getChildren()
	})
</script>

<h1>day 1</h1>
<div>
	{#if children}
		{#each children as child}
			{`${child.name} `}
		{/each}
	{/if}
</div>
<div>
	<input type="text" bind:value={keyword} on:input={() => onSearch(keyword)} />
</div>
<div>
	{result}
</div>
