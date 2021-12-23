<script>
	let tiles = new Array(9).fill('');
	let result = null;
	let player = '⨉';
	const winpattern = [
		[0, 1, 2], //horizontal
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6], //vertical
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 8], //diagonal
		[2, 4, 6]
	];

	function set_tile(index) {
		tiles[index] = player;
		check_result(player);
		console.log(result);
		player = player == '⨉' ? '○' : '⨉';
	}
	function reset() {
		tiles = tiles.map(() => '');
		result = null;
	}
	function check_result(player) {
		if (!tiles.includes('')) result = 'Match Draw';

		winpattern.forEach((pattern) => {
			let current_tiles = [tiles[pattern[0]], tiles[pattern[1]], tiles[pattern[2]]];
			if (current_tiles.every((tile) => tile == player)) {
				// console.log(`Player ${player} Wins!`);
				result = `Player ${player} Wins!`;
			}
		});
	}
</script>

<div class="bg-blue-400 h-screen w-screen grid place-items-center">
	<main
		class="h-full w-full container bg-white sm:h-4/5 flex flex-col justify-around px-8 py-20 sm:rounded-lg"
	>
		<section class="text-5xl text-center font-thiner">
			{#if result === null}
				<p>Player {player}'s turn</p>
			{:else}
				<p>Gameover!</p>
				<p>{result}</p>
			{/if}
		</section>
		<section class="grid grid-cols-3 w-max mx-auto gap-2">
			{#each tiles as tile, index}
				<button
					on:click={() => set_tile(index)}
					disabled={tiles[index] !== ''}
					class="border border-black text-center h-28 sm:h-32 aspect-square sm:hover:bg-black/20 active:bg-black active:text-white rounded text-7xl font-medium grid place-items-center disabled:cursor-not-allowed"
				>
					{tile}
				</button>
			{/each}
		</section>
		<button
			on:click={reset}
			class=" border border-black rounded hover:text-white hover:bg-black text-2xl p-2 font-medium w-max mx-auto"
			>RESET</button
		>
	</main>
</div>
