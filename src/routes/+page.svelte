<script lang="ts">
  import { writable } from 'svelte/store';
  import Counter from '../lib/Counter.svelte';

  let counters = writable([{ id: 1, title: 'Counter 1', count: 0 }]);
  let nextId = 2;
  
  const total = writable(0);

  function addCounter() {
    counters.update(current => [...current, { id: nextId++, title: `Counter ${nextId}`, count: 0 }]);
  }

  function removeCounter(id: number) {
    counters.update(current => {
      const updatedCounters = current.filter(counter => counter.id !== id);
      calculateTotal(updatedCounters);
      return updatedCounters;
    });
  }

  function setCount(id: number, newCount: number) {
    counters.update(current => {
      let updatedCounters = current.map(counter => {
        if (counter.id === id) {
          counter.count = newCount;
        }
        return counter;
      });
      calculateTotal(updatedCounters);
      return updatedCounters;
    });
  }

  function calculateTotal(updatedCounters) {
    const sum = updatedCounters.reduce((acc, { count }) => acc + count, 0);
    total.set(sum);
  }
</script>

<button on:click={addCounter}>new counter</button>

{#each $counters as counter}
  <div>
    <Counter bind:title={counter.title} on:countChanged={(e) => setCount(counter.id, e.detail)} />
    <button on:click={() => removeCounter(counter.id)}>Remove</button>
  </div>
{/each}

<h3>Total: {$total}</h3>
