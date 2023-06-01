<script>
	let keyboard = [
		['Esc', 'F1', 'F2', 'F3', 'F4', 'F5', 'F6', 'F7', 'F8', 'F9', 'F10', 'F11', 'F12'],
		['`', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '-', '=', 'Backspace'],
		['Tab', 'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', '[', ']', '\\'],
		['Caps', 'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', ';', "'", 'Enter'],
		[' Shift', 'Z', 'X', 'C', 'V', 'B', 'N', 'M', ',', '.', 'Shift '],
		[' Ctrl', ' OS', ' Alt', 'Space', 'Alt ', 'OS ', 'Ctrl ', 'Menu']
	];

	let homeBlock = [
		['PrintSc', 'ScrollLock', 'Pause'],
		['Insert', 'Home', 'PageUp'],
		['Delete', 'End', 'PageDown'],
		['Left', 'Up', 'Right', 'Down']
	];

	let numBlock = [
		['Num', ' /', ' *', ' -'],
		[' 7', ' 8', ' 9', ' +'],
		[' 4', ' 5', ' 6'],
		[' 1', ' 2', ' 3'],
		[' 0', ' .', ' Enter']
	];

	let base = 'p-2 border-2 decoration-zinc-500 decoration-2 rounded-xl ';
	let prevPressed = [];
	let currentlyPressed = '';
	let currentlyPressedKey = '';
	let currentlyPressedStyle = 'bg-zinc-600 ';
	let lastPressed = '';

	function replace(x, y) {
		if (currentlyPressed.includes(x)) currentlyPressed = currentlyPressed.replace(x, y);
	}
</script>

<svelte:body
	on:keydown={function (event) {
		event.preventDefault();
		console.log(event.code);
		console.log(event.key);

		currentlyPressed = event.code;
		currentlyPressedKey = event.key;
		console.log(currentlyPressedKey);

		console.log(currentlyPressed);
		replace('Key', '');
		replace('Minus', '-');
		replace('Equal', '=');
		replace('BracketLeft', '[');
		replace('BracketRight', ']');
		replace('Backslash', '\\');
		replace('CapsLock', 'Caps');
		replace('Semicolon', ';');
		replace('Quote', "'");
		replace('ShiftLeft', ' Shift');
		replace('ShiftRight', 'Shift ');
		replace('Comma', ',');
		replace('Period', '.');
		replace('ControlLeft', ' Ctrl');
		replace('OSLeft', ' OS');
		replace('AltLeft', ' Alt');
		replace('AltRight', 'Alt ');
		replace('OSRight', 'OS ');
		replace('ControlRight', 'Ctrl ');
		replace('ContextMenu', 'Menu');
		replace('Escape', 'Esc');
		replace('ArrowLeft', 'Left');
		replace('ArrowUp', 'Up');
		replace('ArrowRight', 'Right');
		replace('ArrowDown', 'Down');
		replace('Backquote', '`');
		replace('NumLock', 'Num');
		replace('PrintScreen', 'PrintSc');
		replace('Digit', '');

		replace('NumpadDivide', ' /');
		replace('NumpadMultiply', ' *');
		replace('NumpadSubtract', ' -');
		replace('NumpadAdd', ' +');
		replace('NumpadDecimal', ' .');
		replace('Numpad', ' ');

		console.log(currentlyPressed);

		lastPressed = currentlyPressed;
		prevPressed.includes(currentlyPressed)
			? (currentlyPressedStyle = ' bg-zinc-300')
			: (currentlyPressedStyle = ' bg-teal-300');
		prevPressed.push(currentlyPressed);
	}}
	on:keyup={function () {
		setTimeout(function () {
			currentlyPressed = null;
		}, 100);
	}}
/>

<p>The key that you pressed was : {lastPressed}</p>
<div class="flex p-4 m-4 border-2 decoration-zinc-500 rounded-xl">
	<section class="p-2 m-2">
		{#each keyboard as row}
			<section class="my-1 flex">
				{#each row as k}
					<kbd
						class={currentlyPressed === k
							? base + 'bg-zinc-600'
							: prevPressed.includes(k)
							? base + 'bg-teal-300'
							: base + 'bg-zinc-300'}>{k}</kbd
					>
				{/each}
			</section>
		{/each}
	</section>

	<section class="p-2 m-2">
		{#each homeBlock as row}
			<section class="my-1 flex">
				{#each row as k}
					<kbd
						class={currentlyPressed === k
							? base + 'bg-zinc-600'
							: prevPressed.includes(k)
							? base + 'bg-teal-300'
							: base + 'bg-zinc-300'}>{k}</kbd
					>
				{/each}
			</section>
		{/each}
	</section>

	<section class="p-2 m-2">
		{#each numBlock as row}
			<section class="my-1 flex">
				{#each row as k}
					<kbd
						class={currentlyPressed === k
							? base + 'bg-zinc-600'
							: prevPressed.includes(k)
							? base + 'bg-teal-300'
							: base + 'bg-zinc-300'}>{k}</kbd
					>
				{/each}
			</section>
		{/each}
	</section>
</div>
