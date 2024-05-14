<!-- MARK: Logic
-->
<script>
  import { createEventDispatcher } from "svelte";

  export let pages;
  export let currentPage;

  const dispatch = createEventDispatcher();
</script>


<!-- MARK: Content
-->
<div class="tabs">
  {#each pages as page}
    <button class:active={currentPage == page.id} class="tab-info" on:click={() => dispatch('clicked', page)}>{page.title}</button>
  {/each}
</div>


<!-- MARK: Styles
-->
<style>
  .tabs {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0.5rem;
    gap: 2rem;
  }
  .tab-info {
    cursor: pointer;
    user-select: none;
    border: none;
    background-color: white;

    transition: color 100ms ease-in-out;
  }
  .tab-info:hover {
    color: #D84727;
  }
  .active {
    color: #D84727;
    border-bottom: 2px solid #D84727;
  }
</style>