<script>
	let keyboard = [
		{
			keys: ['esc', 'F1', 'F2', 'F3', 'F4', 'F5', 'F6', 'F7', 'F8', 'F9', 'F10', 'F11', 'F12']
		},
		{
			keys: ['`', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '-', '=']
		},
		{
			keys: ['tab', 'q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p', '[', ']', '\\']
		},
		{
			keys: ['caps lock', 'a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l', ';', "'", 'enter']
		},
		{
			keys: ['shift', 'z', 'x', 'c', 'v', 'b', 'n', 'm', ',', '.', '/', 'shift']
		},
		{
			keys: ['control', 'option', 'os', ' ', 'os', 'option', 'control']
		}
	];

	let log = '';
	let key;
</script>

<svelte:body
	on:keydown={function (event) {
		event.preventDefault();
		key = event.key;
		log += key.toLowerCase();
	}}
	on:keyup={function () {
		setTimeout(function () {
			key = null;
		}, 100);
	}}
/>

<p class="bg-gray-600 p-4 m-4 w-80 text-zinc-50 mx-auto rounded-xl">{log}</p>
<div class=" p-2 m-4 mx-auto w-min border-zinc-500 border-2 rounded-xl">
	{#each keyboard as block}
		<section class="flex flex-nowrap">
			{#each block.keys as k}
				<button
					class={key === k
						? 'grow text-zinc-300 px-4 py-2 m-2  h-12 rounded-xl ${} border-2 bg-zinc-900 border-zinc-500 duration-300 ease-in-out'
						: log.includes(k)
						? 'grow text-zinc-900 px-4 py-2 m-2  h-12 rounded-xl border-2 bg-teal-300 border-zinc-500 duration-300 ease-in-out'
						: 'grow text-zinc-900 px-4 py-2  m-2  h-12 rounded-xl border-2 bg-zinc-300 border-zinc-500 duration-300 ease-in-out'}
					>{k}</button
				>
			{/each}
		</section>
	{/each}
</div>
