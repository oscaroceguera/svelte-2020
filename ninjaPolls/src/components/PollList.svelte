<script>
  // simport { onMount, onDestroy } from 'svelte';
  import { fade, slide, scale } from 'svelte/transition'
  import { flip } from 'svelte/animate'
  import PollStore from '../stores/PollStore'
  import PollDetail from './PollDetail.svelte'
  
  // const unsub = PollStore.subscribe((data) => {
  //   polls = data;
  // })

  // onMount(() => {
  //   console.log('mountings')
    
  // })

  // onDestroy(() => {
  //   console.log('ondestroy')
  //   unsub()
  // })
</script>

<div class='poll-list'>
  {#each $PollStore as poll (poll.id)}
    <div in:fade out:scale|local animate:flip={{duration: 500}}>
      <PollDetail {poll} />
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>