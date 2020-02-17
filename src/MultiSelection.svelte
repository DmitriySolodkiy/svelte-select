<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let selectedValue = [];
  export let activeSelectedValue = undefined;
  export let isDisabled = false;
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
  .multiSelectItem {
    background: var(--multiItemBG, #EBEDEF);
    margin: var(--multiItemMargin, 5px 5px 0 0);
    border-radius: var(--multiItemBorderRadius, 16px);
    height: var(--multiItemHeight, 32px);
    line-height: var(--multiItemHeight, 32px);
    display: flex;
    cursor: default;
    padding: var(--multiItemPadding, 0 10px 0 15px);
  }

  .multiSelectItem_label {
    margin: var(--multiLabelMargin, 0 5px 0 0);
  }

  .multiSelectItem:hover,
  .multiSelectItem.active {
    background-color: var(--multiItemActiveBG, #006FFF);
    color: var(--multiItemActiveColor, #fff);
  }

  .multiSelectItem.disabled:hover {
    background: var(--multiItemDisabledHoverBg, #EBEDEF);
    color: var(--multiItemDisabledHoverColor, #C1C6CC);
  }

  .multiSelectItem_clear {
    border-radius: var(--multiClearRadius, 50%);
    background: var(--multiClearBG, #52616F);
    width: var(--multiClearWidth, 16px);
    height: var(--multiClearHeight, 16px);
    position: relative;
    top: var(--multiClearTop, 8px);
    text-align: var(--multiClearTextAlign, center);
    padding: var(--multiClearPadding, 1px);
  }

  .multiSelectItem_clear:hover,
  .active .multiSelectItem_clear {
    background: var(--multiClearHoverBG, #fff);
  }

  .multiSelectItem_clear:hover svg,
  .active .multiSelectItem_clear svg {
    fill: var(--multiClearHoverFill, #006FFF);
  }

  .multiSelectItem_clear svg {
    fill: var(--multiClearFill, #EBEDEF);
    vertical-align: top;
  }
</style>
