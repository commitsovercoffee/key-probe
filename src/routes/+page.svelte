<script>
	let keyStatus = new Map();

	const keyMap = [
		{
			Escape: 'Esc',
			F1: 'F1',
			F2: 'F2',
			F3: 'F3',
			F4: 'F4',
			F5: 'F5',
			F6: 'F6',
			F7: 'F7',
			F8: 'F8',
			F9: 'F9',
			F10: 'F10',
			F11: 'F11',
			F12: 'F12'
		},
		{
			Backquote: '~',
			Digit1: '1',
			Digit2: '2',
			Digit3: '3',
			Digit4: '4',
			Digit5: '5',
			Digit6: '6',
			Digit7: '7',
			Digit8: '8',
			Digit9: '9',
			Digit0: '0',
			Minus: '-',
			Equal: '=',
			Backspace: 'Backspace'
		},
		{
			Tab: 'Tab',
			KeyQ: 'Q',
			KeyW: 'W',
			KeyE: 'E',
			KeyR: 'R',
			KeyT: 'T',
			KeyY: 'Y',
			KeyU: 'U',
			KeyI: 'I',
			KeyO: 'O',
			KeyP: 'P',
			BracketLeft: '[',
			BracketRight: ']',
			Backslash: '\\'
		},
		{
			CapsLock: 'Caps',
			KeyA: 'A',
			KeyS: 'S',
			KeyD: 'D',
			KeyF: 'F',
			KeyG: 'G',
			KeyH: 'H',
			KeyJ: 'J',
			KeyK: 'K',
			KeyL: 'L',
			Semicolon: ';',
			Quote: "'",
			Enter: 'Enter'
		},
		{
			ShiftLeft: 'Shift',
			KeyZ: 'Z',
			KeyX: 'X',
			KeyC: 'C',
			KeyV: 'V',
			KeyB: 'B',
			KeyN: 'N',
			KeyM: 'M',
			Comma: ',',
			Period: '.',
			Slash: '/',
			ShiftRight: 'Shift'
		},
		{
			ControlLeft: 'Ctrl',
			OSLeft: 'OS',
			AltLeft: 'Alt',
			Space: 'Space',
			AltRight: 'Alt',
			OSRight: 'OS',
			ControlRight: 'Ctrl',
			Menu: 'Menu'
		}
	];

	const navMap = [
		{
			PrintScreen: 'Print Sc',
			ScrollLock: 'Scrl Lck',
			Pause: 'Pause'
		},
		{
			Insert: 'Ins',
			Home: 'Home',
			PageUp: 'Page Up'
		},
		{
			Delete: 'Del',
			End: 'End',
			pageDown: 'Page Down'
		}
	];

	const navArrow = [
		{
			Fills: 'XX',
			ArrowUp: 'Up',
			Fill: 'XX'
		},
		{
			ArrowLeft: 'Left',
			ArrowDown: 'Down',
			ArrowRight: 'Right'
		}
	];

	const numMap = [
		{
			NumLock: 'Num',
			NumpadDivide: '/',
			NumpadMultiply: '*'
		},

		{
			Numpad7: '7',
			Numpad8: '8',
			Numpad9: '9'
		},
		{
			Numpad4: '4',
			Numpad5: '5',
			Numpad6: '6'
		},
		{
			Numpad1: '1',
			Numpad2: '2',
			Numpad3: '3'
		},
		{
			Numpad0: '0',
			NumpadDecimal: '.'
		}
	];

	let numExtra = [
		{
			NumpadSubtract: '-',
			NumpadAdd: '+',
			NumpadEnter: 'Enter'
		}
	];

	let keyCapStyle =
		'p-2 m-1 border-2 border-zinc-200 dark:border-zinc-800 rounded-xl transition duration-300 delay-50 ';
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
		setTimeout(function () {
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
		}, 50);

		console.log(keyStatus);
	}}
/>

<div class="mx-auto w-fit prose prose-zinc dark:prose-invert max-w-none">
	<div
		class="mt-16 p-4 flex border border-zinc-200 dark:border-zinc-800 rounded-xl flex-grow bg-zinc-50 dark:bg-zinc-800 overflow-hidden"
	>
		<section class="ml-8 mr-8">
			{#each keyMap as row}
				<section class="flex justify-stretch">
					{#each Object.entries(row) as [key, value]}
						{#if value === 'Space'}
							<kbd class={keyCapStyle + 'basis-5/6'} id={key}>{value}</kbd>
						{:else if value === 'Tab' || value === 'Caps' || value === 'Enter'}
							<kbd class={keyCapStyle + 'basis-3/6'} id={key}>{value}</kbd>
						{:else}
							<kbd class={keyCapStyle + 'basis-1/6'} id={key}>{value}</kbd>
						{/if}
					{/each}
				</section>
			{/each}
		</section>

		<div class="flex flex-col justify-between">
			<section class="ml-8 mr-8">
				{#each navMap as row}
					<section class="flex justify-stretch">
						{#each Object.entries(row) as [key, value]}
							{#if value == 'XX'}
								<kbd class={'opacity-0 w-[4rem] h-12 pointer-events-none'} id={key}>{value}</kbd>
							{:else}
								<kbd class={keyCapStyle + 'w-14 h-12 text-xs'} id={key}>{value}</kbd>
							{/if}
						{/each}
					</section>
				{/each}
			</section>

			<section class="ml-8 mr-8">
				{#each navArrow as row}
					<section class="flex justify-stretch">
						{#each Object.entries(row) as [key, value]}
							{#if value == 'XX'}
								<kbd class={'opacity-0 w-[4rem] h-12 pointer-events-none'} id={key}>{value}</kbd>
							{:else}
								<kbd class={keyCapStyle + 'w-14 h-12 text-xs'} id={key}>{value}</kbd>
							{/if}
						{/each}
					</section>
				{/each}
			</section>
		</div>
		<section class="ml-8 mr-8 flex">
			<div>
				{#each numMap as row}
					<section class="flex justify-stretch">
						{#each Object.entries(row) as [key, value]}
							{#if value === '0'}
								<kbd class={keyCapStyle + 'w-[6.5rem] h-12 text-xs'} id={key}>{value}</kbd>
							{:else}
								<kbd class={keyCapStyle + 'w-12 h-12 text-xs'} id={key}>{value}</kbd>
							{/if}
						{/each}
					</section>
				{/each}
			</div>

			<div>
				{#each numExtra as row}
					<section class="flex flex-col">
						{#each Object.entries(row) as [key, value]}
							{#if value === '-'}
								<kbd class={keyCapStyle + 'w-12 h-12 grow-0 text-xs'} id={key}>{value}</kbd>
							{:else}
								<kbd class={keyCapStyle + 'w-12 h-[6.5rem] text-xs'} id={key}>{value}</kbd>
							{/if}
						{/each}
					</section>
				{/each}
			</div>
		</section>
	</div>
</div>
