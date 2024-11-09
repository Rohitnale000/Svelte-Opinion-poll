<script>
  import { createEventDispatcher } from "svelte";
  import Card from "../Sheard/Card.svelte";
  export let poll;

  const dispatch = createEventDispatcher();

  const handleVotes = (option, id) => {
    dispatch("vote", { option, id });
  };

  //reactive value
  $: totalVotes = poll.votesA + poll.votesB;
  $: percentA = Math.floor(100/ totalVotes * poll.votesA)
  $: percentB = Math.floor(100/ totalVotes * poll.votesB)
</script>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>
    <p>Total Votes: {totalVotes}</p>

    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={handleVotes("a", poll.id)}>
      <div class="percent percent-a" style="width: {percentA}%">
        <span>{poll.answerA} <strong>({poll.votesA})</strong></span>
      </div>
    </div>

    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={handleVotes("b", poll.id)}>
      <div class="percent percent-b" style="width: {percentB}%">
        <span>{poll.answerB} <strong>({poll.votesB})</strong></span>
      </div>
    </div>

  </div>
</Card>

<style>
  h3 {
    margin: 0 auto;
    color: #555;
  }
  p {
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }
  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover {
    opacity: 0.6;
  }
  span {
    display: inline-block;
    padding: 10px 20px;
  }
  .percent {
    height: 100%;
    position: relative;
    box-sizing: border-box;
  }
  .percent-a {
    border-left: 4px solid #d91b42;
    background-color: rgb(217, 27, 66,0.2);
  }
  .percent-b {
    border-left: 4px solid #45c496;
    background-color: rgb(69, 196, 150,0.2);
  }
</style>
