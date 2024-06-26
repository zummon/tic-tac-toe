<script>
  let count = $state(0);
  let board = $state([
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ]);
  let ticks = $state([[], [], []]);
  let winner = $state([[], [], []]);

  let place = $derived(count % 2 == 0 ? "x" : "o");

  $effect(() => {
    ticks.forEach((tocks, horz) => {
      tocks.forEach((tock, vert) => {
        if (count - 5 > tock) {
          board[horz][vert] = "";
        }
      });
    });
  });
</script>

<div class="tracking-wider text-center font-serif text-2xl">
  <span class="">Round</span>
  <span class="font-mono font-extrabold">{count}</span>
  <button
    class="underline decoration-2 underline-offset-4 text-yellow-400 focus:text-yellow-600 hover:text-yellow-600 transition disabled:hidden"
    disabled={count == 0}
    onclick={() => {
      board = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ];
      ticks = [[], [], []];
      count = 0;
      winner = [[], [], []];
    }}
  >
    Restart
  </button><br />
  <span class="text-4xl font-extrabold font-mono">{place}</span>
  <span class="">turn</span>
</div>

<div class="grid grid-cols-3 text-6xl font-extrabold font-mono bg-yellow-400 rounded-md">
  {#each board as boxes, horz}
    {#each boxes as box, vert}
      <button
        class="w-20 h-20 overflow-hidden even:border-2 border-yellow-600 transition {count - 5 == ticks[horz][vert]
          ? 'text-yellow-600'
          : 'text-yellow-900'}"
        disabled={box}
        onclick={() => {
          board[horz][vert] = place;
          count++;
          ticks[horz][vert] = count;
        }}
      >
        {box}
      </button>
    {/each}
  {/each}
</div>

<div class="font-serif text-center">
  Made by zummon (Teerapat Anantarattanachai)<br />Something breaks, needs upgrade. Let me know
</div>
