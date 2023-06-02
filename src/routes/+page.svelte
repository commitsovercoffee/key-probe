<script>
	let fnRow = [
		'Esc',
		null,
		'F1',
		'F2',
		'F3',
		'F4',
		null,
		'F5',
		'F6',
		'F7',
		'F8',
		null,
		'F9',
		'F10',
		'F11',
		'F12'
	];

	let main = [
		['`', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '-', '=', 'Backspace'],
		['Tab', 'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', '[', ']', '\\'],
		['Caps', 'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', ';', "'", 'Enter'],
		[' Shift', 'Z', 'X', 'C', 'V', 'B', 'N', 'M', ',', '.', 'Shift '],
		[' Ctrl', ' OS', ' Alt', 'Space', 'Alt ', 'OS ', 'Ctrl ', 'Menu']
	];

	let opts = ['Print Scrn', 'Scroll Lock', 'Pause'];
	let navPad = [
		['Ins', 'Home', 'Page Up'],
		['Del', 'End', 'Page Down']
	];

	let arrows = [
		[null, 'Up', null],
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

	let keyCapStyle =
		'p-0.5 m-1 border-2 border-zinc-200 dark:border-zinc-800 hover:border-zinc-900 hover:dark:border-zinc-100 rounded-lg transition duration-300 delay-50 h-10 ';
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

<div class="mx-auto w-fit prose prose-zinc dark:prose-invert max-w-none">
	<div
		class="m-2 mt-16 p-4 flex border border-zinc-200 dark:border-zinc-800 rounded-xl flex-grow bg-zinc-50 dark:bg-zinc-800 overflow-hidden"
	>
		<section class="p-2 m-2">
			<!-- fnRow -->
			<section class="flex mb-8">
				{#each fnRow as k}
					{#if k === null}
						<kbd class={'opacity-0 w-2/12 no-pointer'}>{k}</kbd>
					{:else}
						<kbd
							class={activeKey === k
								? keyCapStyle + 'w-2/12  ' + 'bg-zinc-600 -translate-y-4 '
								: prevPressed.includes(k)
								? keyCapStyle + 'w-2/12  ' + 'bg-sky-500'
								: keyCapStyle + 'w-2/12  ' + 'bg-zinc-100 dark:bg-zinc-900 '}>{k}</kbd
						>
					{/if}
				{/each}
			</section>

			<!-- main block -->
			<div>
				{#each main as row}
					<section class="my-1 flex">
						{#each row as k}
							{#if k === 'Tab' || k === 'Caps' || k === '\\' || k === 'Enter'}
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
										? keyCapStyle + 'w-3/12 ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-3/12 ' + 'bg-sky-500'
										: keyCapStyle + 'w-3/12 ' + 'bg-zinc-100 dark:bg-zinc-900 '}>{k}</kbd
								>
							{/if}
						{/each}
					</section>
				{/each}
			</div>
		</section>

		<section class="p-2 ml-8 mr-8 m-2">
			<!-- System Control -->

			<section class="flex mb-8">
				{#each opts as k}
					<kbd
						class={activeKey === k
							? keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
							: prevPressed.includes(k)
							? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
							: keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
					>
						<p>
							{k}
						</p>
					</kbd>
				{/each}
			</section>

			<div>
				{#each navPad as row}
					<section class="my-1 flex">
						{#each row as k}
							<kbd
								class={activeKey === k
									? keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
									: prevPressed.includes(k)
									? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
									: keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
							>
								{k}
							</kbd>
						{/each}
					</section>
				{/each}
			</div>

			<div>
				{#each arrows as row}
					<section class="my-1 flex">
						{#each row as k}
							{#if k === null}
								<kbd class={'opacity-0 w-14 no-pointer'}>{k}</kbd>
							{:else}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-12 h-10 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
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

		<div class="p-2 m-2">
			<p class="p-2 mb-8 italic">Commits over coffee.</p>
			<section class="p-2 flex justify-between">
				<div>
					{#each numPad as row}
						<section class="my-1 flex">
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
											? keyCapStyle + 'w-12 h-10 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
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
					<section class="my-1 flex flex-col">
						{#each numExtra as k}
							{#if k === ' -'}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-16 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
										: keyCapStyle + 'w-12 text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
								>
									{k}
								</kbd>
							{:else}
								<kbd
									class={activeKey === k
										? keyCapStyle + 'w-12 h-10 text-xs  ' + 'bg-zinc-600 -translate-y-4 '
										: prevPressed.includes(k)
										? keyCapStyle + 'w-12 text-xs  ' + 'bg-sky-500'
										: keyCapStyle + 'w-12 h-24 text-xs  ' + 'bg-zinc-100 dark:bg-zinc-900 '}
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

	<div class="p-2 m-4 flex justify-between">
		<p class=" text-xl p-2 m-2">
			Last Pressed Key : <kbd>{lastKey}</kbd>
		</p>

		<button
			on:click={function () {
				prevPressed = [];
			}}
			class="px-2 py-1 m-1 bg-[#232323] dark:bg-zinc-900 rounded-xl hover:-translate-y-1 active:translate-y-1 transition duration-50 ease-in shadow-2xl shadow-zinc-800 dark:shadow-zinc-500"
			>Reset</button
		>
	</div>
</div>
