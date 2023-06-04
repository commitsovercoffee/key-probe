<script>
	let baseStyle = 'p-2 m-1 border-2 rounded-xl transition duration-300 border-zinc-200 ';
	let defaultStyle = baseStyle + 'bg-zinc-100 dark:bg-zinc-800 ';
	let keyDownStyle = baseStyle + 'bg-red-300 dark:bg-red-600 -translate-y-4 ';
	let keyUpStyle = baseStyle + 'bg-teal-300 dark:bg-teal-600 ';

	let pressedKeys = new Array();
	let unpressedKeys = new Array();
	let lastKey = [];

	function onKeyDown(e) {
		if (!pressedKeys.includes(e.code)) pressedKeys = [...pressedKeys, e.code];
		console.log('pressedkeys', pressedKeys);
	}

	function onKeyUp(e) {
		setTimeout(function () {
			pressedKeys = [];
			if (!unpressedKeys.includes(e.code)) unpressedKeys = [...unpressedKeys, e.code];
			console.log('unpressedkeys', unpressedKeys);
		}, 50);
	}

	function getWidth(key) {
		switch (key) {
			case 'Space':
				return 'basis-1/2';
			default:
				return 'basis-1/12';
		}
	}

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
			ContextMenu: 'Menu'
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
			PageDown: 'Page Down'
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
</script>

<svelte:window on:keydown|preventDefault={onKeyDown} on:keyup={onKeyUp} />

<div class="mx-auto w-fit prose prose-zinc dark:prose-invert max-w-none">
	<div
		class="mt-16 p-4 flex border border-zinc-200 dark:border-zinc-800 rounded-xl bg-zinc-50 dark:bg-zinc-800"
	>
		<!-- fnRow + 60% -->
		<section>
			{#each keyMap as row}
				<section class="flex">
					{#each Object.entries(row) as [key, value]}
						<kbd
							class={pressedKeys.includes(key)
								? keyDownStyle + getWidth(key)
								: unpressedKeys.includes(key)
								? keyUpStyle + getWidth(key)
								: defaultStyle + getWidth(key)}>{value}</kbd
						>
					{/each}
				</section>
			{/each}
		</section>

		<div>
			<!-- system, nav and arrow keys -->
			<section class="px-8">
				{#each navMap as row}
					<section class="flex justify-stretch text-xs">
						{#each Object.entries(row) as [key, value]}
							<kbd
								class={pressedKeys.includes(key)
									? keyDownStyle + getWidth(key)
									: unpressedKeys.includes(key)
									? keyUpStyle + getWidth(key)
									: defaultStyle + getWidth(key)}>{value}</kbd
							>
						{/each}
					</section>
				{/each}
			</section>

			<!-- arrowBlock -->
			<section class="ml-8 mr-8">
				{#each navArrow as row}
					<section class="flex justify-stretch">
						{#each Object.entries(row) as [key, value]}
							<kbd
								class={pressedKeys.includes(key)
									? keyDownStyle
									: unpressedKeys.includes(key)
									? keyUpStyle
									: defaultStyle}>{value}</kbd
							>
						{/each}
					</section>
				{/each}
			</section>
		</div>
		<!-- numBlock -->
		<section class="ml-8 mr-8">
			{#each numMap as row}
				<section class="flex justify-stretch">
					{#each Object.entries(row) as [key, value]}
						<kbd
							class={pressedKeys.includes(key)
								? keyDownStyle
								: unpressedKeys.includes(key)
								? keyUpStyle
								: defaultStyle}>{value}</kbd
						>
					{/each}
				</section>
			{/each}
		</section>

		<!-- numExtra -->
		<section class="ml-8 mr-8">
			{#each numExtra as row}
				<section class="">
					{#each Object.entries(row) as [key, value]}
						<kbd
							class={pressedKeys.includes(key)
								? keyDownStyle
								: unpressedKeys.includes(key)
								? keyUpStyle
								: defaultStyle}>{value}</kbd
						>
					{/each}
				</section>
			{/each}
		</section>
	</div>

	<div class="m-4 flex justify-between">
		<p class=" text-xl p-2 m-2">
			Last Pressed Key : <kbd>{lastKey}</kbd>
		</p>

		<button
			on:click={function () {
				// Iterate over the map keys
				for (const key in pressedKeys) {
					// Check if the value is true
					if (!pressedKeys[key]) {
						document.getElementById(key).classList.remove('bg-teal-200');
						document.getElementById(key).classList.remove('dark:bg-teal-800');
					}
				}
			}}
			class="px-4 m-1 rounded-xl transition duration-300 delay-50 h-12 bg-zinc-200 dark:bg-zinc-800 hover:-translate-y-1 active:translate-y-1 active:bg-sky-500"
			>Reset</button
		>
	</div>
</div>
