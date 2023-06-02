<script>
	export let keys;
	export let activeKey = '';
	export let prevPressed = [];
</script>

<section class="p-2 m-2">
	{#each keys as row}
		<section class="my-1 flex">
			{#each row as k}
				<kbd
					class={activeKey === k
						? KeyCapStyle + 'bg-zinc-600 -translate-y-4 text-zinc-100'
						: prevPressed.includes(k)
						? KeyCapStyle + 'bg-sky-500'
						: KeyCapStyle + 'bg-zinc-300'}>{k}</kbd
				>
			{/each}
		</section>
	{/each}
</section>
