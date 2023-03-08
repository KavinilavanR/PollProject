<script>
  import { createEventDispatcher } from "svelte";
  export let items;
  export let activeItem = "Current Poll(s)";
  const dispatch = createEventDispatcher();
</script>

<ul>
  {#each items as item}
    <li on:click={() => dispatch("switchTab", item)}>
      <div class:active={item === activeItem}>{item}</div>
    </li>
  {/each}
</ul>

<style>
  ul {
    display: flex;
    flex-direction: row;
    list-style-type: none;
    padding: 0px;
  }
  li {
    margin: 0 16px;

    font-size: 18px;
    cursor: pointer;
  }
  .active {
    border-bottom: 2px solid red;
    padding-bottom: 6px;
    color: red;
  }
</style>
