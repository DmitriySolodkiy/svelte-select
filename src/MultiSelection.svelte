<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let selectedValue = [];
  export let getSelectionLabel = undefined;

  function handleClear(i, event) {
    event.stopPropagation();
    dispatch('multiItemClear', {i});
  }
</script>

<div class="multiSelectItems">
  {#each selectedValue as value, i}
    {@html getSelectionLabel(value)}{#if i+1 != selectedValue.length},&nbsp{/if}
  {/each}
</div>

<style>
  .multiSelectItems {
    flex-flow: row nowrap;
    white-space: nowrap;
    height: available;
    overflow: hidden;
    padding-top: 5px;
    color: #000000;
    text-overflow: ellipsis;
    width: var(--multiItemsWidth, 340px);
  }
</style>
