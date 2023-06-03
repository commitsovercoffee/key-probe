<script>
	import { element } from 'svelte/internal';

	let main = [
		[
			'Esc',
			'keyFill',
			'F1',
			'F2',
			'F3',
			'F4',
			'keyFill',
			'F5',
			'F6',
			'F7',
			'F8',
			'keyFill',
			'F9',
			'F10',
			'F11',
			'F12'
		],
		['rowFill'],
		['`', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '-', '=', 'Backspace'],
		['Tab', 'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', '[', ']', '\\'],
		['Caps', 'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', ';', "'", 'Enter'],
		[' Shift', 'Z', 'X', 'C', 'V', 'B', 'N', 'M', ',', '.', 'Shift '],
		[' Ctrl', ' OS', ' Alt', 'Space', 'Alt ', 'OS ', 'Ctrl ', 'Menu']
	];

	let navPad = [
		['Print Scrn', 'Scroll Lock', 'Pause'],
		['rowFill'],
		['Ins', 'Home', 'Page Up'],
		['Del', 'End', 'Page Down'],
		['keyFill'],
		['keyFill'],
		['keyFill', 'Up', 'keyFill'],
		['Left', 'Down', 'Right']
	];

	let numPad = [
		['Num', ' /', ' *'],
		[' 7', ' 8', ' 9'],
		[' 4', ' 5', ' 6'],
		[' 1', ' 2', ' 3'],
		[' 0', ' .']
	];
	let numExtra = [' -', ' +', ' Enter'];

	let prevPressed = [];
	let activeKey = '';
	let activeCode = '';
	let lastKey = '';

	let map = {};
	console.log(map);

	let keyCapStyle =
		'p-1 m-1 border-2 border-zinc-200 dark:border-zinc-800 rounded-xl transition duration-300 delay-50 h-12 ';
</script>

<svelte:body
	on:keydown={function (event) {
		map[event.code] = element.type == this['on:keydown'];
		console.log(map);

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
			activeKey = 'keyFill';
		}, 100);
	}}
/>

<div class="mx-auto w-fit prose prose-zinc dark:prose-invert max-w-none">
	<div
		class="mt-16 p-4 flex border border-zinc-200 dark:border-zinc-800 rounded-xl flex-grow bg-zinc-50 dark:bg-zinc-800 overflow-hidden"
	>
		<section class="">
			<!-- main block -->
			<div>
				{#each main as row}
					<section class="flex">
						{#each row as k}
							{#if k === 'rowFill'}
								<kbd class={'h-10 w-full no-pointer'} />
							{:else if k === 'keyFill'}
								<kbd class={'opacity-0 w-12 no-pointer'}>{k}</kbd>
							{:else if k === 'Tab' || k === 'Caps' || k === '\\' || k === 'Enter'}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-4/12 ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-4/12 ' + 'bg-sky-500'
										: keyCapStyle + 'w-4/12 ' + 'bg-zinc-100 dark:bg-zinc-900 '}>{k}</kbd
								>
							{:else if k === 'Backspace' || k === ' Shift' || k === 'Shift '}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-5/12 ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-5/12 ' + 'bg-sky-500'
										: keyCapStyle + 'w-5/12 ' + 'bg-zinc-100 dark:bg-zinc-900 '}>{k}</kbd
								>
							{:else if k === 'Space'}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-10/12 ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-10/12 ' + 'bg-sky-500'
										: keyCapStyle + 'w-10/12 ' + 'bg-zinc-100 dark:bg-zinc-900 '}>{k}</kbd
								>
							{:else}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-3/12 ' + 'bg-red-300 dark:bg-red-500 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-3/12 ' + 'bg-teal-300 dark:bg-teal-800 prose-invert'
										: keyCapStyle + 'w-3/12 ' + 'bg-zinc-100 dark:bg-zinc-900 '}>{k}</kbd
								>
							{/if}
						{/each}
					</section>
				{/each}
			</div>
		</section>

		<section class="ml-8 mr-8">
			<!-- System Control -->
			<div>
				{#each navPad as row}
					<section class="flex">
						{#each row as k}
							{#if k === 'rowFill'}
								<kbd class={'h-10 w-full no-pointer'} />
							{:else if k === 'keyFill'}
								<kbd class={'opacity-0 w-14 no-pointer'}>{k}</kbd>
							{:else}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
										: keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
								>
									{k}
								</kbd>
							{/if}
						{/each}
					</section>
				{/each}
			</div>
		</section>

		<div>
			<p class="m-8 text-xs italic">Designed & developed by<br />Commits over coffee.</p>
			<section class="flex justify-center">
				<div class="p-0 m-0">
					{#each numPad as row}
						<section class="flex">
							{#each row as k}
								{#if k === ' 0'}
									<kbd
										class={activeKey === k
											? keyCapStyle + 'w-16 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
											: prevPressed.includes(k)
											? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
											: keyCapStyle + 'grow text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
									>
										{k}
									</kbd>
								{:else}
									<kbd
										class={activeKey === k
											? keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
											: prevPressed.includes(k)
											? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
											: keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
									>
										{k}
									</kbd>
								{/if}
							{/each}
						</section>
					{/each}
				</div>
				<div>
					<section class="flex flex-col p-0 m-0 h-full">
						{#each numExtra as k}
							{#if k === ' -'}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
										: keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
								>
									{k}
								</kbd>
							{:else}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
										: keyCapStyle + 'w-12 grow text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
								>
									{k}
								</kbd>
							{/if}
						{/each}
					</section>
				</div>
			</section>
		</div>
	</div>

	<div class="m-4 flex justify-between">
		<p class=" text-xl p-2 m-2">
			Last Pressed Key : <kbd>{lastKey}</kbd>
		</p>

		<button
			on:click={function () {
				prevPressed = [];
			}}
			class="px-4 m-1 rounded-xl transition duration-300 delay-50 h-12 bg-zinc-200 dark:bg-zinc-800 hover:-translate-y-1 active:translate-y-1 active:bg-sky-500"
			>Reset</button
		>
	</div>
</div>
