<script lang="ts">
  function sleep(ms: number) {
      return new Promise(resolve => setTimeout(resolve, ms));
  }
  
  export let nums: Array<number>;
  $: scaled = nums.map((x: number) => x/Math.max(...nums)*100);
  export let algo: number;

  let selected: number | null;
  let algos: { [id:number] : string } = {
    0: "Insertion Sort",
    1: "Bubble Sort",
    2: "Count Sort"
  }
  let functions: { [id:number] : Function } = {
    0: async () => {
        console.log("insertionSort started")
        console.log("nums:", nums)
        let size = nums.length;
        let j;
        for (let i = 1; i < size; i++) {
            j = i;
            while ((j > 0) && (nums[j-1] > nums[j])) {
            selected = j - 1;
            let tmp = nums[j-1];
            nums[j-1] = nums[j];
            nums[j] = tmp;
            await sleep(1000/nums.length)
            j--;
            }
        } selected = null;},
    1: async () => {
        console.log("bubbleSort started")
        console.log("nums:", nums)
        let size = nums.length;
        let swapped = true;
        while (swapped) {
            swapped = false;
            for (let i=1; i < size; i++) {
                selected = i;
                if (nums[i-1] > nums[i]) {
                    let tmp = nums[i-1];
                    nums[i-1] = nums[i];
                    nums[i] = tmp;
                    swapped = true;
                    await sleep(1000/nums.length)
                }
            }
        }
        selected = null;
    }
  }
</script>
<div class="container">
  <span>
    {algos[algo]}
  </span>
  <div class="nums-container">
    {#each scaled as num, i}
      {#if i == selected}
        <div class="number-bar" style="width:{num}%; background-color: darkblue;"/>
      {:else}
        <div class="number-bar" style="width:{num}%;"/>
      {/if}
    {/each}
  </div>
  <div class="btn" on:click="{functions[algo]()}">
    Sort Items
  </div>
</div>


<style>
  .container {
    display: flex;
    flex-direction: column;
    background-color: #f9f9f9;
    padding: .5em;
    margin: 1em;
    min-height: 300px;
    min-width: 300px;
  }
  span {
    font-size:large;
    font-weight:800;
  }
  .nums-container {
    display: flex;
    flex-direction: column;
    flex-wrap:nowrap;
    flex: 1 1 auto;
  }
  .number-bar {
    margin: .5px;
    background-color: blue;
    min-height: .1px;
    flex: 1 1 auto;
  }
</style>