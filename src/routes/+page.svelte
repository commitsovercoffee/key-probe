<script>
	let keyStatus = new Map();

	let keyCapStyle =
		'p-1 m-1 border-2 border-zinc-200 dark:border-zinc-800 rounded-xl transition duration-300 delay-50 h-12 bg-zinc-100 ';

	let fnRow = [
		['KeyQ', 'KeyW', 'KeyE'],
		['KeyA', 'KeyS', 'KeyD']
	];
</script>

<svelte:body
	on:keydown={function (event) {
		event.preventDefault();

		keyStatus[event.code] = true;

		for (const key in keyStatus) {
			if (keyStatus.hasOwnProperty(key)) {
				// Check if the value is true
				if (keyStatus[key]) {
					document.getElementById(key).classList.remove('bg-zinc-100');
					document.getElementById(key).classList.remove('bg-teal-300');
					document.getElementById(key).classList.add('bg-red-300');
					document.getElementById(key).classList.add('-translate-y-2');
				}
			}
		}

		console.log(keyStatus);
	}}
	on:keyup={function (event) {
		event.preventDefault();

		keyStatus[event.code] = false;

		for (const key in keyStatus) {
			if (keyStatus.hasOwnProperty(key)) {
				// Check if the value is true
				if (!keyStatus[key]) {
					document.getElementById(key).classList.remove('bg-red-300');
					document.getElementById(key).classList.add('bg-teal-300');
					document.getElementById(key).classList.remove('-translate-y-2');
				}
			}
		}

		console.log(keyStatus);
	}}
/>

<div class="mx-auto w-fit prose prose-zinc dark:prose-invert max-w-none">
	<div
		class="mt-16 p-4 flex border border-zinc-200 dark:border-zinc-800 rounded-xl flex-grow bg-zinc-50 dark:bg-zinc-800 overflow-hidden"
	>
		<section class="ml-8 mr-8">
			{#each fnRow as row}
				<section class="flex">
					{#each row as k}
						<kbd id={k} class={keyCapStyle}>
							{k}
						</kbd>
					{/each}
				</section>
			{/each}
		</section>
	</div>
</div>
