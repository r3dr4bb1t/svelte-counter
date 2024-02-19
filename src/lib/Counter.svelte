<script lang="ts">
  export let title: string = 'Multiple Counter';
  let count: number = 0;

  function increment() {
    count += 1;
  }

  function decrement() {
    count -= 1;
  }

  function reset() {
    count = 0;
  }
</script>

<div>
  <h2>{title}</h2>
  <button on:click={decrement}>-</button>
  <span>{count}</span>
  <button on:click={increment}>+</button>
  <button on:click={reset}>Reset</button>
</div>
