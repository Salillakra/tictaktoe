<script>
  let Xturn = true;
  let board = Array(9).fill("");

  const winPatterns = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8], // Rows
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8], // Columns
    [0, 4, 8],
    [2, 4, 6], // Diagonals
  ];

  const checkWinner = (player) => {
    for (const pattern of winPatterns) {
      const [a, b, c] = pattern;
      if (board[a] === player && board[b] === player && board[c] === player) {
        return true;
      }
    }
    return false;
  };

  const handleClick = (e, index) => {
    if (!board[index]) {
      board[index] = Xturn ? "X" : "O";
      Xturn = !Xturn;
    }

    if (checkWinner("X")) {
      alert("Player X wins!");
      resetGame();
    } else if (checkWinner("O")) {
      alert("Player O wins!");
      resetGame();
    }
  };

  const handleKeyPress = (event, index) => {
    if (event.key === "Enter" || event.key === " ") {
      handleClick(null, index);
    }
  };

  const resetGame = () => {
    board = Array(9).fill("");
    Xturn = true;
  };
</script>

<h1 class="text-center">Tick Tac Toe</h1>

<div
  class="text-center w-[20rem] rounded-xl mx-auto mt-24 text-3xl bg-slate-400 p-3"
>
  Tic Tac Toe
</div>

<div class="grid grid-cols-[repeat(3,6rem)] gap-3 my-5 justify-center">
  {#each board as cell, index (index)}
    <span
      class="w-24 h-24 focus:border border-white bg-slate-600 text-7xl flex justify-center items-center"
      role="button"
      tabindex="0"
      on:click={(e) => handleClick(e, index)}
      on:keydown={(e) => handleKeyPress(e, index)}
    >
      {cell}
    </span>
  {/each}
</div>
<button class="mx-auto block" on:click={resetGame}>Reset Game</button>
