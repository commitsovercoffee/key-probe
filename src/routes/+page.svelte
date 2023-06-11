<script>
	import { slide } from 'svelte/transition';

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
			{ key: 'OS', keycode: 'MetaLeft' },
			{ key: 'Alt', keycode: 'AltLeft' },
			{ key: 'Space', keycode: 'Space' },
			{ key: 'Alt', keycode: 'AltRight' },
			{ key: 'OS', keycode: 'MetaRight' },
			{ key: 'Ctrl', keycode: 'ControlRight' },
			{ key: 'Menu', keycode: 'ContextMenu' }
		]
	];

	let navKeys = [
		[
			{ key: 'Print Sc', keycode: 'PrintScreen' },
			{ key: 'Scrl Lck', keycode: 'ScrollLock' },
			{ key: 'Pause', keycode: 'Pause' }
		],

		[
			{ key: 'Ins', keycode: 'Insert' },
			{ key: 'Home', keycode: 'Home' },
			{ key: 'Page Up', keycode: 'PageUp' }
		],

		[
			{ key: 'Del', keycode: 'Delete' },
			{ key: 'End', keycode: 'End' },
			{ key: 'Page Down', keycode: 'PageDown' }
		]
	];

	let arrowKeys = [
		[
			{ key: '', keycode: 'Fill' },
			{ key: 'Up', keycode: 'ArrowUp' },
			{ key: '', keycode: 'Fill' }
		],

		[
			{ key: 'Left', keycode: 'ArrowLeft' },
			{ key: 'Down', keycode: 'ArrowDown' },
			{ key: 'Right', keycode: 'ArrowRight' }
		]
	];

	let numKeys = [
		[
			{ key: 'Num', keycode: 'NumLock' },
			{ key: '/', keycode: 'NumpadDivide' },
			{ key: '*', keycode: 'NumpadMultiply' }
		],
		[
			{ key: '7', keycode: 'Numpad7' },
			{ key: '8', keycode: 'Numpad8' },
			{ key: '9', keycode: 'Numpad9' }
		],
		[
			{ key: '4', keycode: 'Numpad4' },
			{ key: '5', keycode: 'Numpad6' },
			{ key: '6', keycode: 'Numpad9' }
		],
		[
			{ key: '1', keycode: 'Numpad1' },
			{ key: '2', keycode: 'Numpad2' },
			{ key: '3', keycode: 'Numpad3' }
		],
		[
			{ key: '0', keycode: 'Numpad0' },
			{ key: '.', keycode: 'NumpadDecimal' }
		]
	];

	let numExtra = [
		{ key: '-', keycode: 'NumpadSubtract' },
		{ key: '+', keycode: 'NumpadAdd' },
		{ key: 'Ent', keycode: 'NumpadEnter' }
	];
	let keysPressed = [];
	let prevPressed = [];
	let log = [];

	let keyCapStyle =
		'p-2 m-1 rounded-xl border-2 border-zinc-200 dark:border-zinc-800 h-12 transition-all duration-200 transform grow ';
	let keyDownStyle =
		' bg-amber-200 dark:bg-amber-800 text-zinc-800 dark:text-zinc-200 transform -translate-y-10';
	let keyUpStyle = ' bg-teal-200 dark:bg-teal-800';
	let keyDefaultStyle = ' bg-zinc-100 dark:bg-zinc-900 ';

	const handleKeyDown = (event) => {
		log = [...log, { key: event.key, code: event.code }];

		if (!keysPressed.some((item) => item.code === event.code)) {
			keysPressed = [...keysPressed, { key: event.key, code: event.code }];
		}
	};

	const handleKeyUp = (event) => {
		if (!prevPressed.some((item) => item.code === event.code)) {
			prevPressed = [...prevPressed, { key: event.key, code: event.code }];
		}

		keysPressed = keysPressed.filter((item) => item.code !== event.code);
	};

	function getStyle(key) {
		switch (key) {
			case 'NumpadSubtract':
				return keyCapStyle + ' grow-0 ';
			case 'NumpadEnter':
				return keyCapStyle + ' grow ';
			case 'NumpadAdd':
				return keyCapStyle + ' grow ';
			case 'Fill':
				return keyCapStyle + ' opacity-0 ';
			case 'Space':
				return keyCapStyle + ' basis-8/12 ';
			default:
				return keyCapStyle + '  basis-1/12 ';
		}
	}
</script>

<svelte:window on:keydown|preventDefault={handleKeyDown} on:keyup|preventDefault={handleKeyUp} />

<main class="mx-auto w-fit prose prose-zinc dark:prose-invert max-w-none">
	<div
		class="mt-16 py-4 px-2 border border-zinc-200 dark:border-zinc-800 rounded-xl bg-zinc-50 dark:bg-zinc-800"
	>
		<div class="flex h-min">
			<!-- 60% keys -->
			<div class="flex flex-col w-min h-min">
				{#each keyboard as row}
					<div class="flex p-1">
						{#each row as key}
							<div
								class={keysPressed.some((item) => item.code === key.keycode)
									? getStyle(key.keycode) + keyDownStyle
									: prevPressed.some((item) => item.code === key.keycode)
									? getStyle(key.keycode) + keyUpStyle
									: getStyle(key.keycode) + keyDefaultStyle}
							>
								{key.key}
							</div>
						{/each}
					</div>
				{/each}
			</div>

			<!-- navKeys -->
			<div class="flex flex-col w-min justify-between text-xs">
				<div>
					{#each navKeys as row}
						<div class="flex p-1">
							{#each row as key}
								<div
									class={keysPressed.some((item) => item.code === key.keycode)
										? getStyle(key.keycode) + keyDownStyle
										: prevPressed.some((item) => item.code === key.keycode)
										? getStyle(key.keycode) + keyUpStyle
										: getStyle(key.keycode) + keyDefaultStyle}
								>
									{key.key}
								</div>
							{/each}
						</div>
					{/each}
				</div>
				<div>
					{#each arrowKeys as row}
						<div class="flex p-1">
							{#each row as key}
								<div
									class={keysPressed.some((item) => item.code === key.keycode)
										? getStyle(key.keycode) + keyDownStyle
										: prevPressed.some((item) => item.code === key.keycode)
										? getStyle(key.keycode) + keyUpStyle
										: getStyle(key.keycode) + keyDefaultStyle}
								>
									{key.key}
								</div>
							{/each}
						</div>
					{/each}
				</div>
			</div>

			<div class="flex self-end">
				<div class="flex flex-col">
					{#each numKeys as row}
						<div class="flex p-1 text-xs">
							{#each row as key}
								<div
									class={keysPressed.some((item) => item.code === key.keycode)
										? getStyle(key.keycode) + keyDownStyle + 'w-10'
										: prevPressed.some((item) => item.code === key.keycode)
										? getStyle(key.keycode) + keyUpStyle + 'w-10'
										: getStyle(key.keycode) + keyDefaultStyle + 'w-10'}
								>
									{key.key}
								</div>
							{/each}
						</div>
					{/each}
				</div>

				<div class="flex flex-col p-1 text-xs">
					{#each numExtra as key}
						<div
							class={keysPressed.some((item) => item.code === key.keycode)
								? getStyle(key.keycode) + keyDownStyle + 'w-10'
								: prevPressed.some((item) => item.code === key.keycode)
								? getStyle(key.keycode) + keyUpStyle + 'w-10'
								: getStyle(key.keycode) + keyDefaultStyle + 'w-10'}
						>
							{key.key}
						</div>
					{/each}
				</div>
			</div>
		</div>
	</div>

	<div class="my-4 flex justify-between">
		<section class="p-1 m-2 flex">
			<kbd class="p-2 m-2 border-none">Log :</kbd>
			<div class="flex flex-col-reverse">
				{#each log as val}
					<kbd in:slide|local out:slide|local class={keyCapStyle + keyDefaultStyle + ' grow-0'}
						>{val.code}</kbd
					>
				{/each}
			</div>
		</section>

		<button
			on:click={function () {
				prevPressed = [];
				log = [];
			}}
			class="p-2 m-1 basis-1/6 rounded-xl h-min transition duration-300 bg-zinc-200 dark:bg-zinc-800 hover:bg-stone-300 hover:dark:bg-stone-600 active:bg-slate-300 active:dark:bg-slate-600 active:translate-y-1"
			>Reset</button
		>
	</div>
</main>
