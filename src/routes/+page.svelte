<script>
	let oneU = 'px-4 py-2 m-1';
	let twoU = 'px-8 py-2 m-1';
	let threeU = 'px-16 py-2 m-1';
	let growU = 'px-2 py-2 m-1 grow';

	let letter = 'px-6 py-2 m-1';
	let fill = 'grow';

	let keyCap = 'rounded-xl border-2 border-zinc-500 duration-300 ease-in-out ';
	let unpressed = ' bg-zinc-500';
	let pressed = ' bg-red-500';
	let prevpressed = ' bg-teal-500';

	let fnRow = [
		{ legend: 'Esc', key: 'Escape', size: oneU, filler: null },
		{ legend: '', key: '', size: oneU, filler: fill },
		{ legend: 'F1', key: 'F1', size: oneU, filler: null },
		{ legend: 'F2', key: 'F2', size: oneU, filler: null },
		{ legend: 'F3', key: 'F3', size: oneU, filler: null },
		{ legend: 'F4', key: 'F4', size: oneU, filler: null },
		{ legend: '', key: '', size: oneU, filler: fill },
		{ legend: 'F5', key: 'F5', size: oneU, filler: null },
		{ legend: 'F6', key: 'F6', size: oneU, filler: null },
		{ legend: 'F7', key: 'F7', size: oneU, filler: null },
		{ legend: 'F8', key: 'F8', size: oneU, filler: null },
		{ legend: '', key: '', size: oneU, filler: fill },
		{ legend: 'F9', key: 'F9', size: oneU, filler: null },
		{ legend: 'F10', key: 'F10', size: oneU, filler: null },
		{ legend: 'F11', key: 'F11', size: oneU, filler: null },
		{ legend: 'F12', key: 'F12', size: oneU, filler: null }
	];

	let mainBlock = [
		[
			{ legend: 'tab', key: 'Tab', size: twoU, filler: null },
			{ legend: 'q', key: 'q', size: letter, filler: null },
			{ legend: 'w', key: 'w', size: letter, filler: null },
			{ legend: 'e', key: 'e', size: letter, filler: null },
			{ legend: 'r', key: 'r', size: letter, filler: null },
			{ legend: 't', key: 't', size: letter, filler: null },
			{ legend: 'y', key: 'y', size: letter, filler: null },
			{ legend: 'u', key: 'u', size: letter, filler: null },
			{ legend: 'i', key: 'i', size: letter, filler: null },
			{ legend: 'o', key: 'o', size: letter, filler: null },
			{ legend: 'p', key: 'p', size: letter, filler: null },
			{ legend: '[', key: '[', size: letter, filler: null },
			{ legend: ']', key: ']', size: letter, filler: null },
			{ legend: '\\', key: '\\', size: twoU, filler: null }
		],
		[
			{ legend: 'caps', key: 'Caplock', size: twoU, filler: null },
			{ legend: 'a', key: 'a', size: letter, filler: null },
			{ legend: 's', key: 's', size: letter, filler: null },
			{ legend: 'd', key: 'd', size: letter, filler: null },
			{ legend: 'f', key: 'f', size: letter, filler: null },
			{ legend: 'g', key: 'g', size: letter, filler: null },
			{ legend: 'h', key: 'h', size: letter, filler: null },
			{ legend: 'j', key: 'j', size: letter, filler: null },
			{ legend: 'k', key: 'k', size: letter, filler: null },
			{ legend: 'l', key: 'l', size: letter, filler: null },
			{ legend: ';', key: ';', size: letter, filler: null },
			{ legend: "'", key: "'", size: letter, filler: null },
			{ legend: 'enter', key: 'enter', size: twoU, filler: null }
		],
		[
			{ legend: 'shift', key: 'Shift', size: growU, filler: null },
			{ legend: 'z', key: 'z', size: letter, filler: null },
			{ legend: 'x', key: 'x', size: letter, filler: null },
			{ legend: 'c', key: 'c', size: letter, filler: null },
			{ legend: 'v', key: 'v', size: letter, filler: null },
			{ legend: 'b', key: 'b', size: letter, filler: null },
			{ legend: 'n', key: 'n', size: letter, filler: null },
			{ legend: 'm', key: 'm', size: letter, filler: null },
			{ legend: ',', key: ',', size: letter, filler: null },
			{ legend: '.', key: '.', size: letter, filler: null },
			{ legend: '/', key: '/', size: letter, filler: null },
			{ legend: 'shift', key: 'Shift', size: growU, filler: null }
		],
		[
			{ legend: 'ctrl', key: 'Control', size: oneU, filler: null },
			{ legend: 'os', key: 'OS', size: oneU, filler: null },
			{ legend: 'alt', key: 'Alt', size: oneU, filler: null },
			{ legend: '', key: ' ', size: growU, filler: null },
			{ legend: 'alt', key: 'Alt', size: oneU, filler: null },
			{ legend: 'os', key: 'OS', size: oneU, filler: null },
			{ legend: 'menu', key: 'ContextMenu', size: oneU, filler: null },
			{ legend: 'ctrl', key: 'Control', size: oneU, filler: null }
		]
	];
	let log = '';
	let key;
</script>

<svelte:body
	on:keydown={function (event) {
		event.preventDefault();
		key = event.key;
		log += key;
	}}
	on:keyup={function () {
		setTimeout(function () {
			key = null;
		}, 100);
	}}
/>

<p class="bg-gray-600 p-4 m-4 text-zinc-50 mx-auto rounded-xl">{log}</p>
<div class="p-2 m-4 w-fit mx-auto border-zinc-500 border-2 rounded-xl">
	<section class="flex flex-nowrap">
		{#each fnRow as k}
			{#if k.filler != null}
				<div class={k.filler} />
			{:else}
				<button
					class={key === k.key
						? keyCap + k.size + pressed
						: log.includes(k.key)
						? keyCap + k.size + prevpressed
						: keyCap + k.size + unpressed}>{k.legend}</button
				>
			{/if}
		{/each}
	</section>

	{#each mainBlock as block}
		<section class="flex flex-nowrap">
			{#each block as k}
				{#if k.filler != null}
					<div class={k.filler} />
				{:else}
					<button
						class={key === k.key
							? keyCap + k.size + pressed
							: log.includes(k.key)
							? keyCap + k.size + prevpressed
							: keyCap + k.size + unpressed}>{k.legend}</button
					>
				{/if}
			{/each}
		</section>
	{/each}
</div>
