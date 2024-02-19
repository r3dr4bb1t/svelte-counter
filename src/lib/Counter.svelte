<script lang="ts">
  export let title: string;
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

  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  $: dispatch('countChanged', count);
</script>

<div>
  <input type="text" bind:value={title} />
  <button on:click={decrement}>-</button>
  <span>{count}</span>
  <button on:click={increment}>+</button>
  <button on:click={reset}>Reset</button>
</div>
