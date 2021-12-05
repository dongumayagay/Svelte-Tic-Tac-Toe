<script>
	let tiles = ['', '', '', '', '', '', '', '', ''];
	// let tiles = ['0', '1', '2', '3', '4', '5', '6', '7', '8'];

	let winner = null;

	let player = '⨉';
	function change_tile(index) {
		tiles[index] = player;
		check_winner(player);
		player = player == '⨉' ? '○' : '⨉';
	}
	function reset() {
		tiles = tiles.map(() => '');
		winner = null;
	}
	let winpattern = [
		[0, 1, 2], //horizontal
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6], //vertical
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 8], //diagonal
		[2, 4, 6]
	];
	function check_winner(player) {
		winpattern.forEach((pattern) => {
			let current_tiles = [tiles[pattern[0]], tiles[pattern[1]], tiles[pattern[2]]];

			if (current_tiles.every((tile) => tile == player)) {
				// console.log(`${player} win`);
				winner = player;
			}
		});
	}
</script>

<div class="bg-blue-400 h-screen w-screen grid place-items-center">
	<main
		class="h-full w-full bg-white sm:h-4/5 sm:w-3/4 flex flex-col justify-around px-8 py-20 sm:rounded-lg"
	>
		<section class="text-5xl text-center font-thiner">
			{#if !winner}
				<p>Player {player}'s turn</p>
			{:else}
				<p>Gameover!</p>
				<p>Player {winner} wins</p>
			{/if}
		</section>
		<section class="grid grid-cols-3 gap-2 w-full">
			{#each tiles as tile, index}
				<button
					on:click={() => change_tile(index)}
					disabled={tiles[index] !== ''}
					class="border border-black text-center h-28 sm:hover:bg-black/20 active:bg-black active:text-white rounded text-7xl font-medium grid place-items-center disabled:cursor-not-allowed"
				>
					{tile}
				</button>
			{/each}
		</section>
		<button
			on:click={reset}
			class=" border border-black my-2 rounded hover:text-white hover:bg-black text-2xl p-2 font-medium"
			>RESET</button
		>
	</main>
</div>
