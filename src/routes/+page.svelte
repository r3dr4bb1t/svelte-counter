<script lang="ts">
  import Counter from '../lib/Counter.svelte';
  let counters: Array<{ id: number; title: string }> = [
    { id: 1, title: 'Counter 1' },
  ];
  let nextId = 2;

  function addCounter() {
    counters = [...counters, { id: nextId++, title: `Counter ${nextId}` }];
  }

  function removeCounter(id: number) {
    counters = counters.filter(counter => counter.id !== id);
  }
</script>

<button on:click={addCounter}>new counter</button>

{#each counters as { id, title }}
  <div>
    <Counter {title} />
    <button on:click={() => removeCounter(id)}>Remove</button>
  </div>
{/each}
