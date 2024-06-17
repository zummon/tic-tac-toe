<script>
  let count = $state(0);
  let board = $state([
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ]);
  let ticks = $state([[], [], []]);

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

<div class="tracking-wider text-center font-serif text-3xl">
  <span class="">Round</span>
  <span class="font-mono font-extrabold text-yellow-400">{count}</span>
  <button
    class="text-yellow-600"
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
  </button>
</div>

<div
  class="grid grid-cols-3 text-6xl font-extrabold font-mono bg-yellow-400 text-yellow-900 absolute inset-0 w-fit h-fit m-auto z-30"
>
  {#each board as boxes, horz}
    {#each boxes as box, vert}
      <button
        class="w-20 h-20 even:border-2 border-yellow-600"
        disabled={box}
        onclick={() => {
          if (count % 2 == 0) {
            board[horz][vert] = "x";
          } else {
            board[horz][vert] = "o";
          }
          count++;
          ticks[horz][vert] = count;
        }}
      >
        {box}
      </button>
    {/each}
  {/each}
</div>

<div class="font-serif absolute bottom-0 inset-x-0 text-center">
  Made by zummon (Teerapat Anantarattanachai)<br />Something breaks, needs upgrade. Let me know
</div>
