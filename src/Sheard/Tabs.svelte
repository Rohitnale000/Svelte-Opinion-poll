<script>
  import { createEventDispatcher } from "svelte";

  export let items;
  export let activeItem;

  const dispatch = createEventDispatcher();
</script>

<div class="container text-center mt-5">
  <ul class="list-inline">
    {#each items as item}
      <li
        class="list-inline-item mx-3 fs-5 text-secondary"
        on:click={() => dispatch('tabChange', item)}
      >
        <div class:active={item === activeItem}>
          {item}
        </div>
      </li>
    {/each}
  </ul>
</div>

<style>
  .active {
    color: #d91b42;
    border-bottom: 2px solid #d91b42;
  }
  li {
    cursor: pointer;
  }
</style>
