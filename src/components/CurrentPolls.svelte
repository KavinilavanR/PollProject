<script>
  import PollDetails from "./PollDetails.svelte";

    export let pollObject =[];
    console.log("hii");
        // console.log('current',pollObject[0].pollName);
</script>
<div class = 'poll-object'>
{#each pollObject as poll(poll.id)}
<PollDetails {poll} on:vote/>
{/each}
</div>
<style>
    .poll-object{
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    width:100%;
    height:auto;
  }
</style>