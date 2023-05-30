<script>
	let keyboard = ['a', 'b', 'c', 'd', 'e'];
	let log = '';
	let key;
</script>

<svelte:window
	on:keydown={function (event) {
		key = event.key;
		log += key;
	}}
	on:keyup={function () {
		setTimeout(function () {
			key = null;
		}, 100);
	}}
/>

<div class="mx-auto w-80">
	<p class="bg-gray-600 w-80 h-80 text-zinc-50">{log}</p>

	{#each keyboard as k}
		<button
			class={key === k
				? 'text-zinc-300 px-4 py-2 m-2 rounded-xl border-2 bg-zinc-900 border-zinc-500 duration-300 ease-in-out'
				: log.includes(k)
				? 'text-zinc-900 px-4 py-2 m-2 rounded-xl border-2 bg-teal-300 border-zinc-500 duration-300 ease-in-out'
				: 'text-zinc-900 px-4 py-2 m-2 rounded-xl border-2 bg-zinc-300 border-zinc-500 duration-300 ease-in-out'}
			>{k}</button
		>
	{/each}
</div>
