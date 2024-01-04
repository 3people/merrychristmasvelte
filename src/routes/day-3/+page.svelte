<script lang="ts">
	import { onMount } from 'svelte'

	interface ChildrenInfo {
		name: string
		weight: number
	}

	let childrenList: ChildrenInfo[]
	let giftList: ChildrenInfo[] = []
	$: sum = giftList.map((element) => element.weight).reduce((a, b) => a + b, 0)

	async function fetchChildrenList() {
		const response = await fetch(
			'https://advent.sveltesociety.dev/data/2023/day-three.json',
			{
				method: 'GET'
			}
		)

		return response.json()
	}

	function addToGiftList(index: number) {
		if (sum + childrenList[index].weight > 100) {
			alert(`IT'S TOO HEAVY`)
			return
		}
		giftList = [...giftList, childrenList[index]]
		childrenList.splice(index, 1)
		childrenList = childrenList
	}

	function addToChildrenList(index: number) {
		childrenList = [...childrenList, giftList[index]]
		giftList.splice(index, 1)
		giftList = giftList
	}

	onMount(async () => {
		childrenList = await fetchChildrenList()
	})
</script>

<div class="flex h-full w-full gap-8 p-8">
	<div>
		{#if childrenList}
			<table class="bg-black">
				<thead class="text-xs font-normal uppercase">
					<tr class="[&>th]:pb-4">
						<th class="px-16">name</th>
						<th class="px-8">weight</th>
						<th>let them gift!</th>
					</tr>
				</thead>
				<tbody>
					{#each childrenList as info, i}
						<tr class="[&>td]:py-2">
							<td>{info.name}</td>
							<td>{info.weight}</td>
							<td
								class="cursor-pointer text-center"
								on:click={() => addToGiftList(i)}
							>
								🎁
							</td>
						</tr>
					{/each}
				</tbody>
			</table>
		{/if}
	</div>
	<div>
		{#if giftList}
			<table class="bg-black">
				<thead class="text-xs font-normal uppercase">
					<tr class="[&>th]:pb-4">
						<th class="px-16">name</th>
						<th class="px-8">weight</th>
						<th>drop</th>
					</tr>
				</thead>
				<tbody>
					{#each giftList as info, i}
						<tr class="[&>td]:py-2">
							<td>{info.name}</td>
							<td>{info.weight}</td>
							<td
								class="cursor-pointer text-center"
								on:click={() => addToChildrenList(i)}
							>
								❌
							</td>
						</tr>
					{/each}
				</tbody>
			</table>
		{/if}
	</div>
</div>
