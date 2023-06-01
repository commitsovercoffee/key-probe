<script>
	import KeyCap from './keyCap.svelte';
	let main = [
		['Esc', 'F1', 'F2', 'F3', 'F4', 'F5', 'F6', 'F7', 'F8', 'F9', 'F10', 'F11', 'F12'],
		['`', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '-', '=', 'Backspace'],
		['Tab', 'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', '[', ']', '\\'],
		['Caps', 'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', ';', "'", 'Enter'],
		[' Shift', 'Z', 'X', 'C', 'V', 'B', 'N', 'M', ',', '.', 'Shift '],
		[' Ctrl', ' OS', ' Alt', 'Space', 'Alt ', 'OS ', 'Ctrl ', 'Menu']
	];

	let navPad = [
		['PrintSc', 'ScrollLock', 'Pause'],
		['Insert', 'Home', 'PageUp'],
		['Delete', 'End', 'PageDown'],
		['Left', 'Up', 'Right', 'Down']
	];

	let numPad = [
		['Num', ' /', ' *', ' -'],
		[' 7', ' 8', ' 9', ' +'],
		[' 4', ' 5', ' 6'],
		[' 1', ' 2', ' 3'],
		[' 0', ' .', ' Enter']
	];

	let prevPressed = [];
	let activeKey = '';
	let activeCode = '';
	let lastKey = '';
</script>

<svelte:body
	on:keydown={function (event) {
		event.preventDefault();
		activeKey = event.code;
		activeCode = event.key;

		function replace(x, y) {
			if (activeKey.includes(x)) activeKey = activeKey.replace(x, y);
		}

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

		prevPressed.push(activeKey);
		lastKey = activeKey;
		console.log(prevPressed);
	}}
	on:keyup={function () {
		setTimeout(function () {
			activeKey = null;
		}, 100);
	}}
/>

<div class="mx-auto w-fit">
	<p class="text-xl p-2 m-2">
		Last Pressed Key : <kbd>{lastKey}</kbd>
	</p>
	<div class="flex p-2 m-2 border-2 decoration-red-500 rounded-xl">
		<KeyCap keys={main} {activeKey} {prevPressed} />
		<KeyCap keys={navPad} {activeKey} {prevPressed} />
		<KeyCap keys={numPad} {activeKey} {prevPressed} />
	</div>
</div>
