<script lang="ts">
  import Sort from './Sort.svelte';
  import Slider from '@bulatdashiev/svelte-slider';

  let len = [10, 100];
  let nums: Array<number> = Array.from({length: len[0]}, () => Math.floor(Math.random() * len[0]));
  $: nums = Array.from({length: len[0]}, () => Math.floor(Math.random() * len[0]));
  $: insertionNums = nums.slice();
  $: bubbleNums = nums.slice();

  function sortAll() {}
</script>

<main>
  <h1>Sorting Algorithms</h1>
  Count: {len[0]}
  <Slider bind:value={len} min={5} max={250}/>
  <div class="sortbtn" on:click={sortAll()}>
    Sort All
  </div>
  <div class="sort-container">
    <Sort algo={0} nums={insertionNums} numsOG={nums} />
    <Sort algo={1} nums={bubbleNums} numsOG={nums} />
  </div>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
  main {
    text-align: center;
    padding-top: 1em;
    /* margin: 0 auto; */
  }
  h1 {
    color: #5B8C5A;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 500;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }
  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }
  /* .sort-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(2, 1fr);
    grid-column-gap: 0px;
    grid-row-gap: 0px;
  } */
  .sort-container {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    height: max-content;
    align-items: flex-start;
    justify-content: center;
  }
</style>
