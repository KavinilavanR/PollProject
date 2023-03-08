<script>
  import Card from "../shared/Card.svelte";
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

//   import { each } from "svelte/internal";

export let poll=[];
let totalVotes = 0;
let percentage={};
console.log('poll',poll);

$: {
    totalVotes =0;
    for (const [key, value] of Object.entries(poll.optionvalues)) {
    console.log(`${key}: ${value}`);
    totalVotes+=value;
    }
    for (const [key, value] of Object.entries(poll.optionvalues)) {
    percentage[key] = 0;
    if(totalVotes!=0)
   { percentage[key] = Math.floor((value/totalVotes)*100);
    console.log(`${key}: ${value} : ${totalVotes}`);
   }
}




}// totalVotes
const increaseVote = (name, key, value) => {
    // poll.optionvalues[key] = value+1;
    const pollData ={
       name,
        key,
        value,
        // id:Math.random()
    };
    dispatch('vote',pollData);
}
</script>

<Card>
  <div class="poll">
    <div class="poll-name"><h3>{poll.pollName}</h3></div>
    <div class="total-votes">Total Votes = {totalVotes}</div>
    <div class="poll-options">
      {#each Object.entries(poll.optionvalues) as [key, value], i}
        <div
          class="poll-option"
          on:click={() => {
            increaseVote(poll.pollName, key, value);
          }}
        > <div class="percent percent-{i}" style="width: {percentage[key]}%"></div>
          <span>{key}-{value}</span>
        </div>
      {/each}
    </div>
  </div>
</Card>

<style>
  .total-votes {
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }
  .poll {
    margin: 20px;
  }
  .poll-name {
    margin: 0 auto;
    color: #555;
  }
  .poll-option {
      height: 40px;
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .poll-option:hover {
    opacity: 0.6;
  }
  .percent{
    height: 100%;
    position: absolute;
    box-sizing: border-box;
  }
  .percent-0{
    background: rgba(217,27,66,0.2);
    border-left: 4px solid #d91b42;
  }
  .percent-1{
    background: rgba(69,196,150,0.2);
    border-left: 4px solid #45c496;
  }
  span{
    padding: 10px;
  }
</style>
