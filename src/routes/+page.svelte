<script>
	const keyboard = [
		// Row 0
		[
			{ key: 'Esc', keycode: 'Escape' },
			{ key: 'F1', keycode: 'F1' },
			{ key: 'F2', keycode: 'F2' },
			{ key: 'F3', keycode: 'F3' },
			{ key: 'F4', keycode: 'F4' },
			{ key: 'F5', keycode: 'F5' },
			{ key: 'F6', keycode: 'F6' },
			{ key: 'F7', keycode: 'F7' },
			{ key: 'F8', keycode: 'F8' },
			{ key: 'F9', keycode: 'F9' },
			{ key: 'F10', keycode: 'F10' },
			{ key: 'F11', keycode: 'F11' },
			{ key: 'F12', keycode: 'F12' }
		],

		// Row 1
		[
			{ key: '`', keycode: 'Backquote' },
			{ key: '1', keycode: 'Digit1' },
			{ key: '2', keycode: 'Digit2' },
			{ key: '3', keycode: 'Digit3' },
			{ key: '4', keycode: 'Digit4' },
			{ key: '5', keycode: 'Digit5' },
			{ key: '6', keycode: 'Digit6' },
			{ key: '7', keycode: 'Digit7' },
			{ key: '8', keycode: 'Digit8' },
			{ key: '9', keycode: 'Digit9' },
			{ key: '0', keycode: 'Digit0' },
			{ key: '-', keycode: 'Minus' },
			{ key: '=', keycode: 'Equal' },
			{ key: 'Backspace', keycode: 'Backspace' }
		],
		// Row 2
		[
			{ key: 'Tab', keycode: 'Tab' },
			{ key: 'Q', keycode: 'KeyQ' },
			{ key: 'W', keycode: 'KeyW' },
			{ key: 'E', keycode: 'KeyE' },
			{ key: 'R', keycode: 'KeyR' },
			{ key: 'T', keycode: 'KeyT' },
			{ key: 'Y', keycode: 'KeyY' },
			{ key: 'U', keycode: 'KeyU' },
			{ key: 'I', keycode: 'KeyI' },
			{ key: 'O', keycode: 'KeyO' },
			{ key: 'P', keycode: 'KeyP' },
			{ key: '[', keycode: 'BracketLeft' },
			{ key: ']', keycode: 'BracketRight' },
			{ key: '\\', keycode: 'Backslash' }
		],
		// Row 3
		[
			{ key: 'Caps', keycode: 'CapsLock' },
			{ key: 'A', keycode: 'KeyA' },
			{ key: 'S', keycode: 'KeyS' },
			{ key: 'D', keycode: 'KeyD' },
			{ key: 'F', keycode: 'KeyF' },
			{ key: 'G', keycode: 'KeyG' },
			{ key: 'H', keycode: 'KeyH' },
			{ key: 'J', keycode: 'KeyJ' },
			{ key: 'K', keycode: 'KeyK' },
			{ key: 'L', keycode: 'KeyL' },
			{ key: ';', keycode: 'Semicolon' },
			{ key: "'", keycode: 'Quote' },
			{ key: 'Enter', keycode: 'Enter' }
		],
		// Row 4
		[
			{ key: 'Shift', keycode: 'ShiftLeft' },
			{ key: 'Z', keycode: 'KeyZ' },
			{ key: 'X', keycode: 'KeyX' },
			{ key: 'C', keycode: 'KeyC' },
			{ key: 'V', keycode: 'KeyV' },
			{ key: 'B', keycode: 'KeyB' },
			{ key: 'N', keycode: 'KeyN' },
			{ key: 'M', keycode: 'KeyM' },
			{ key: ',', keycode: 'Comma' },
			{ key: '.', keycode: 'Period' },
			{ key: '/', keycode: 'Slash' },
			{ key: 'Shift', keycode: 'ShiftRight' }
		],
		// Row 5
		[
			{ key: 'Ctrl', keycode: 'ControlLeft' },
			{ key: 'MetaLeft', keycode: 'MetaLeft' },
			{ key: 'Alt', keycode: 'AltLeft' },
			{ key: 'Space', keycode: 'Space' },
			{ key: 'Alt', keycode: 'AltRight' },
			{ key: 'Ctrl', keycode: 'ControlRight' }
		]
	];

	let keysPressed = [];
	let keyCapStyle =
		'key h-8 bg-gray-300 grow text-gray-700 font-bold rounded-md p-2 mx-1 transition-all duration-200 transform ';

	const handleKeyDown = (event) => {
		if (!keysPressed.some((item) => item.code === event.code)) {
			keysPressed = [...keysPressed, { key: event.key, code: event.code }];
		}
	};

	const handleKeyUp = (event) => {
		keysPressed = keysPressed.filter((item) => item.code !== event.code);
	};
</script>

<svelte:window on:keydown|preventDefault={handleKeyDown} on:keyup|preventDefault={handleKeyUp} />

<main class="min-h-screen flex items-center justify-center bg-gray-200">
	<div class="flex flex-col justify-center flex-wrap">
		{#each keyboard as row}
			<div class="key-group flex space-x-2 p-2">
				{#each row as key}
					<div
						class={keysPressed.some((item) => item.code === key.keycode)
							? keyCapStyle + ' bg-red-500 text-white transform -translate-y-8'
							: keyCapStyle}
					>
						{key.key}
					</div>
				{/each}
			</div>
		{/each}
	</div>
</main>

