<script>
  import Sort from './Sort.svelte'
  let nums = Array.from({length: 40}, () => Math.floor(Math.random() * 40));
  let insertionNums = nums.slice();
  let bubbleNums = nums.slice();
  let countNums = nums.slice();
</script>

<main>
  <h1>Sorting Algorithms</h1>
  <div class="sortbtn" on:click=>

  </div>
  <div class="sort-container">
    <Sort algo={0} nums={insertionNums}/>
    <Sort algo={1} nums={bubbleNums}/>
    <Sort algo={2} nums={countNums}/>
  </div>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
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
