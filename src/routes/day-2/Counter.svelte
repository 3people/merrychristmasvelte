<script lang="ts">
	let count = 0

	const increment = () => {
		count += 1
	}

	const decrement = () => {
		if (count <= 0) {
			return
		}
		count -= 1
	}

	const reset = () => {
		count = 0
	}
</script>

<div class="flex border-collapse items-center gap-1 bg-white">
	<button class="h-16 w-16" on:click={decrement}>-</button>
	<div class="flex h-16 w-32 items-center justify-center px-4">
		{count}
		{count > 0 ? 'Cookies' : 'Cookie'}
	</div>
	<button class="h-16 w-16" on:click={increment}>+</button>
</div>
<div>
	<button on:click={reset}>reset</button>
</div>
