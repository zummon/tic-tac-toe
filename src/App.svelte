<script>
  let xo = ['','','','','','','','','']
  let result = ['','']

  $: {
    let prepare = ''
    if (xo[0] == xo[3] && xo[3] == xo[6] && xo[0] && xo[3] && xo[6]) {
      prepare = xo[0]
    } else if (xo[1] == xo[4] && xo[4] == xo[7] && xo[1] && xo[4] && xo[7]) {
      prepare = xo[1]
    } else if (xo[2] == xo[5] && xo[5] == xo[8] && xo[2] && xo[5] && xo[8]) {
      prepare = xo[2]
    } else if (xo[0] == xo[4] && xo[4] == xo[8] && xo[0] && xo[4] && xo[8]) {
      prepare = xo[0]

    } else if (xo[0] == xo[1] && xo[1] == xo[2] && xo[0] && xo[1] && xo[2]) {
      prepare = xo[0]
    } else if (xo[3] == xo[4] && xo[4] == xo[5] && xo[3] && xo[4] && xo[5]) {
      prepare = xo[3]
    } else if (xo[6] == xo[7] && xo[7] == xo[8] && xo[6] && xo[7] && xo[8]) {
      prepare = xo[6]
    } else if (xo[2] == xo[4] && xo[4] == xo[6] && xo[2] && xo[4] && xo[6]) {
      prepare = xo[2]
    } 
    
    if (xo.filter((box) => box).length >= 9 && !prepare) {
      result = ['' , 'Tie !']
    } else {
      result = [prepare, prepare ? 'wins !' : '']
    }
  }
</script>

<div class="cursor-default tracking-wider">
  <span class="text-6xl font-mono font-extrabold text-[#e7bb63]">{result[0]}</span>
  <span class="text-3xl text-white font-serif">{result[1]}</span>
</div>

<div class="grid grid-cols-3 divide-x divide-y divide-yellow-600 bg-[#e7bb63] my-4">
  {#each xo as box, index (index)}
    <button class="w-20 h-20 text-6xl font-extrabold text-yellow-900 font-mono block {box ? '' : 'hover:bg-yellow-600 focus:bg-yellow-600'}" on:click={() => {
      if (!box) {
        let x = xo.filter((box) => box == 'x').length
        let o = xo.filter((box) => box == 'o').length
        if (x > o) {
          box = 'o'
        } else {
          box = 'x'
        }
      }
    }}>{box}</button>
  {/each}
</div>

<button class="text-3xl text-yellow-600 font-mono" on:click={() => {
  xo = ['','','','','','','','','']
}}>
  Reset
</button>

<div class="font-serif mt-8 text-lime-800">Made by zummon (Teerapat Anantarattanachai)<br>Something breaks, shows incorrect result. Let me know.</div>