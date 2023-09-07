<script lang="ts">
  
  function sleep(ms: number) {
      return new Promise(resolve => setTimeout(resolve, ms));
  }
  
  export let nums: Array<number>;
  export let numsOG: Array<number>;
  $: scaled = nums.map((x: number) => x/Math.max(...nums)*100);
  export let algo: number;

  let sorting: boolean = false;
  export let selected: number | null;
  let algos: { [id:number] : string } = {
    0: "Insertion Sort",
    1: "Bubble Sort",
    2: "Count Sort"
  }
  let f: Array<number> = [];
  function factorial(n: number) : number {
    if (n == 0 || n == 1)
      return 1;
    if (f[n] > 0)
      return f[n];
    return f[n] = factorial(n-1) * n;
  }
  let functions: { [id:number] : Function } = {
    0: async () => {
        sorting = true;
        console.log("insertionSort started")
        console.log("nums:", nums)
        let size = nums.length;
        let j;
        for (let i = 1; i < size && sorting; i++) {
            j = i;
            while ((j > 0) && (nums[j-1] > nums[j])) {
            selected = j - 1;
            let tmp = nums[j-1];
            nums[j-1] = nums[j];
            nums[j] = tmp;
            // let fac = Math.sqrt(factorial(nums.length));
            await sleep(1000/size);
            j--;
            }
        } selected = null;},
    1: async () => {
        sorting = true;
        console.log("bubbleSort started")
        console.log("nums:", nums)
        let size = nums.length;
        let swapped = true;
        while (swapped) {
            swapped = false;
            for (let i=1; i < size && sorting; i++) {
                selected = i;
                if (nums[i-1] > nums[i]) {
                    let tmp = nums[i-1];
                    nums[i-1] = nums[i];
                    nums[i] = tmp;
                    swapped = true;
                    await sleep(1000/size);
                }
            }
        }
        selected = null;
    },
    99: async () => {
      sorting = false;
      nums = [...numsOG]
      console.log("reset nums", nums)
    }
  }
</script>
<div class="container" style="height: {10*nums.length}px">
  <span>
    {algos[algo]}
  </span>
  <div class="nums-container">
    {#each scaled as num, i}
      {#if i == selected}
        <div class="number-bar" style="width:{num}%; background-color: #5B8C5A;"/>
      {:else}
        <div class="number-bar" style="width:{num}%;"/>
      {/if}
    {/each}
  </div>
  <button class="btn" on:click={() => functions[algo]()}>
    Sort Items
  </button>
  <button class="btn" on:click={() => functions[99]()}>
    Reset Items
  </button>
</div>


<style>
  .btn {
    background-color: inherit;
    color: white;
    font-weight: 600;
    border-radius: 1em 1em 0 0;
  }
  .btn:nth-child(even) {
    border-radius: 0 0 1em 1em;
  }
  .btn:hover {
    background-color: #5B8C5A;
  }
  .container {
    background-color: #292F36;
    color: #EAEBED;
    border-radius: 2em;
    display: flex;
    flex-direction: column;
    padding: .5em;
    margin: 1em;
    min-height: 300px;
    max-height: 600px;
    min-width: 300px;
    flex: auto;
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
    margin-bottom: 1em;
    max-height: 500px;
  }
  .number-bar {
    margin: .5px;
    background-color: #5BA75B;
    min-width: 1px;
    min-height: .5px;
    flex: 1 1 auto;
  }
</style>