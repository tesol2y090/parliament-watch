<script lang="ts">
	import { Checkbox, Search } from 'carbon-components-svelte';
	import type { VotingSummary } from '../../routes/assemblies/[id]/votes/+page';
	import type { VotesFilter } from './shared';
	export let votes: VotingSummary[] = [];
	export let filter: VotesFilter;
	let resultFilter = filter.result;
	let catergoryFilter = filter.category;

	const getRowCountFilteredByCategory = (category: string) => {
		let result = 0;
		for (let i = 0; i < votes.length; i++) {
			if (votes[i].categories.includes(category)) {
				result++;
			}
		}
		return result;
	};

	const getRowCountFilteredByResult = (label: string) => {
		let result = 0;
		for (let i = 0; i < votes.length; i++) {
			if (votes[i].result === label) {
				result++;
			}
		}
		return result;
	};

	const resetFilter = () => {
		filter = {
			name: '',
			result: [],
			category: []
		};
	};
</script>

<div class="max-w-unset md:max-w-[256px] relative flex flex-col justify-between">
	<div class="px-[24px]">
		<Search
			placeholder="ค้นหาชื่อมติ/คำที่เกี่ยวข้อง"
			bind:value={filter.name}
			light
			class="sticky top-0"
		/>
		<div class="mt-[16px]">
			<span class="label-01 text-gray-60">ผลลัพท์</span>
			{#each resultFilter as value}
				<Checkbox bind:group={filter.result} {value}>
					<div slot="labelText">
						<span class="body-01">{value}</span>
						<span class="body-01 text-gray-60">({getRowCountFilteredByResult(value)})</span>
					</div>
				</Checkbox>
			{/each}
		</div>
		<div class="mt-[16px]">
			<span class="label-01 text-gray-60">ผลลัพท์</span>
			{#each catergoryFilter as value}
				<Checkbox bind:group={filter.category} {value}>
					<div slot="labelText">
						<span class="body-01">{value}</span>
						<span class="body-01 text-gray-60">({getRowCountFilteredByCategory(value)})</span>
					</div>
				</Checkbox>
			{/each}
		</div>
	</div>
	<button
		class="bottom-[0px] p-[14px] w-full text-blue-90 border-blue-70 boder-solid border hover:cursor-pointer text-left"
		on:click={resetFilter}
	>
		ล้างตัวเลือก
	</button>
</div>

<style></style>
