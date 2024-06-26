<script>
  let count = $state(0);
  let board = $state([
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ]);
  let ticks = $state([[], [], []]);
  let winner = $state("");

  $effect(() => {
    ticks.forEach((tocks, horz) => {
      tocks.forEach((tock, vert) => {
        if (count - 5 > tock) {
          board[horz][vert] = "";
        }
      });
      const mark = board[horz][1];
      if (board[horz][0] == mark && mark == board[horz][2]) {
        winner = mark;
      }
    });
  });
</script>

<div class="tracking-wider text-center font-serif text-2xl">
  <span class="">Round</span>
  <span class="font-mono font-extrabold">{count}</span>
  <button
    class="border-b-2 border-yellow-400 text-yellow-400 focus:text-yellow-600 hover:text-yellow-600 focus:border-yellow-600 hover:border-yellow-600 transition"
    disabled={count == 0}
    onclick={() => {
      board = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ];
      ticks = [[], [], []];
      count = 0;
    }}
  >
    Restart
  </button><br />
  {winner}
</div>

<div class="grid grid-cols-3 text-6xl font-extrabold font-mono bg-yellow-400 rounded-md">
  {#each board as boxes, horz}
    {#each boxes as box, vert}
      {@const place = count % 2 == 0 ? "x" : "o"}
      <button
        class="w-20 h-20 overflow-hidden even:border-2 border-yellow-600 transition {box
          ? 'text-yellow-900'
          : 'text-transparent hover:text-yellow-600 focus:text-yellow-600'}"
        disabled={box}
        onclick={() => {
          board[horz][vert] = place;
          count++;
          ticks[horz][vert] = count;
        }}
      >
        {box || place}
      </button>
    {/each}
  {/each}
</div>

<div class="font-serif text-center">
  Made by zummon (Teerapat Anantarattanachai)<br />Something breaks, needs upgrade. Let me know
</div>
