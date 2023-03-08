<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../shared/Button.svelte";
  const dispatch = createEventDispatcher();
  let noOfOptions = 2;
  let optionValues = [];
  let optionVoteMapping = {};
  const addNoOfOptions = () => {
    console.log("here");
    noOfOptions++;
    // optionValues = Array(noOfOptions);
    console.log("");
  };
  const createNewPoll = () => {
    optionValues.forEach((option) => {
      optionVoteMapping[option] = 0;
    });
    const pollObject = {
      pollName,
      optionvalues: optionVoteMapping,
      id: Math.random(),
    };
    console.log(pollObject);
    dispatch("addNewPoll", pollObject);
  };

  let pollName;
</script>

<form class="add-new-pole-form" on:submit|preventDefault>
  <div class="poll-name">
    <label for="poll-name">Poll Name</label>
    <input type="text" name="poll-name" id="poll-name" bind:value={pollName} />
  </div>
  <label>Poll options</label>
  <div class="poll-options">
    {#each Array(noOfOptions) as _, i}
      <input
        type="text"
        name="poll-option-{i}"
        id="poll-option-{i}"
        bind:value={optionValues[i]}
      />
    {/each}
  </div>
  <Button type="primary" on:click={addNoOfOptions}>Add more poll option</Button>
  <Button on:click={createNewPoll}>Create Poll</Button>
</form>

<style>
  /* main{
          position: fixed;
    display: flex;
    gap:5px;
    height: 100%;
    width: 100%;
    background: red;
    flex-direction: column;
    opacity: 0.5;
    align-items: center;
    justify-content: center;
    } */
  label {
    font-size: 20px;
  }
  input[type="text"] {
    /* border:none;
        border-bottom: 2px solid black;
         */
    /* box-shadow: 1px 2px 3px rgba(0,0,0,0.2); */
    border-radius: 5px;
    font-size: 16px;
  }

  .add-new-pole-form {
    /* position: fixed; */
    display: flex;
    width: 300px;
    gap: 5px;
    /* height: 100%;
    width: 100%; */
    background: white;
    /* color:red; */
    flex-direction: column;
    /* border: 2px solid black; */
    padding: 40px 20px;
    /* border-radius: 10px; */
    /* box-shadow: 1px 2px 3px rgba(0,0,0,0.2); */
    opacity: 1;
    /* align-items: center; */
    /* justify-content: ; */
  }
  .poll-name {
    display: flex;
    gap: 5px;
    flex-direction: column;
  }
  .poll-options {
    display: flex;
    gap: 4px;
    flex-direction: column;
  }
</style>
