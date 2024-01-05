<script lang="ts">
	import { onMount } from 'svelte'

	let promise = getHeartRate()

	function handlePromise() {
		promise = getHeartRate()
	}

	async function getHeartRate() {
		const response = await fetch(
			'https://advent.sveltesociety.dev/data/2023/day-four.json',
			{
				method: 'GET'
			}
		)

		return await response.json()
	}

	onMount(() => {
		setInterval(() => {
			handlePromise()
		}, 1000)
	})
</script>

<div class="flex h-full w-full flex-col items-center justify-center">
	<div class="absolute top-0 text-2xl">Santa’s Heart Rate Monitor (SHRM™)</div>
	{#await promise then info}
		<div class="text-3xl text-green-400">
			{info.heartRate}
		</div>
	{/await}
</div>
