<script>
  import AddNewPoll from "./components/AddNewPoll.svelte";
  import CurrentPolls from "./components/CurrentPolls.svelte";
  import Footer from "./components/Footer.svelte";
  import Header from "./components/Header.svelte";
  import Tabs from "./shared/Tabs.svelte";
  // import './../public/img/poll-svgrepo-com.svg'
  let items = ["Current Poll(s)", "Add New Poll"];
  let activeItem = "Current Poll(s)";
  let pollObject = [];
  const switchTab = (e) => {
    activeItem = e.detail;
  };

  const addNewPoll = (e) => {
    console.log(e.detail);
    pollObject = [e.detail, ...pollObject];
    console.log(pollObject);
    activeItem = "Current Poll(s)";
  };
  const handleVote = (e) => {
	  console.log("hereee",e.detail);
    const { name, key, value } = e.detail;
    let copiedPolls = [...pollObject];
    let upvotedPoll = copiedPolls.find((poll) => poll.pollName == name);
	upvotedPoll.optionvalues[key] = value+1;

    pollObject = copiedPolls;
  };
</script>

<body>
  <div class="home-page">
    <Header />
    <Tabs {items} {activeItem} on:switchTab={switchTab} />
    {#if activeItem === "Current Poll(s)"}
      <CurrentPolls {pollObject} on:vote={handleVote} />
    {:else}
      <AddNewPoll on:addNewPoll={addNewPoll} />
    {/if}
  </div>
  <Footer />
</body>

<style>
  body {
    margin: 0px;
    border: 0px;
  }
  .home-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    width: auto;
    gap: 20px;
    justify-content: flex-start;
  }
</style>
