<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../shared/Button.svelte";
  const dispatch = createEventDispatcher();
  let noOfOptions = 2;
  let optionValues = [];
  let optionVoteMapping = {};
  const addNoOfOptions = () => {
    noOfOptions++;
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
    dispatch("addNewPoll", pollObject);
  };

  let pollName;
</script>

<form class="add-new-pole-form" on:submit|preventDefault>
  <div class="poll-name">
    <label for="poll-name">Poll Name</label>
    <input type="text" name="poll-name" id="poll-name" bind:value={pollName} />
  </div>
  <label for ='poll-options'>Poll options</label>
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
  label {
    font-size: 20px;
  }
  input[type="text"] {
    border-radius: 5px;
    font-size: 16px;
  }

  .add-new-pole-form {
    display: flex;
    width: 300px;
    gap: 5px;
    background: white;
    flex-direction: column;
    padding: 40px 20px;
    opacity: 1;
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
