<script>
  function struct(pass) {
    if (pass == "") {
      return [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ];
    }
    return [[], [], []];
  }
  let count = $state(0);
  let board = $state(struct(""));
  let ticks = $state(struct());

  let place = $derived(count % 2 == 0 ? "x" : "o");

  $effect(() => {
    console.log("unticking");
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
      board = struct("");
      ticks = struct();
      count = 0;
    }}
  >
    Restart
  </button><br />
  <span class="text-4xl font-extrabold font-mono">{place}</span>
  <span class="">turn</span>
</div>

<div class="text-6xl font-extrabold font-mono bg-yellow-400 border border-yellow-600">
  {#each board as boxes, horz}
    <div class="flex">
      {#each boxes as box, vert}
        <button
          class="w-20 h-20 overflow-hidden border border-yellow-600 transition enabled:hover:bg-yellow-600 enabled:focus:bg-yellow-600 {count -
            5 ==
          ticks[horz][vert]
            ? 'text-yellow-600'
            : 'text-yellow-900'}"
          disabled={count - 5 <= ticks[horz][vert]}
          onclick={() => {
            board[horz][vert] = place;
            count++;
            ticks[horz][vert] = count;
          }}
        >
          {box}
        </button>
      {/each}
    </div>
  {/each}
</div>

<div class="font-serif text-center">
  Made by zummon (Teerapat Anantarattanachai)<br />Something breaks, needs upgrade. Let me know
</div>

Try {board.flatMap((pose) => pose).join("")}
