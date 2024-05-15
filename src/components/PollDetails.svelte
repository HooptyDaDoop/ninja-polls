<script>
  import { createEventDispatcher } from "svelte";

  export let poll = {};

  const dispatch = createEventDispatcher();

  const addVote = (option, id) => {
    dispatch("vote", { option, id });
  };

  $: totalVotes = poll.votesA + poll.votesB;

  $: percentA = Math.floor((100 / totalVotes) * poll.votesA);
  $: percentB = Math.floor((100 / totalVotes) * poll.votesB);
</script>

<div class="details">
  <div class="answer-a votes" on:keydown={() => {}} on:click={() => addVote("a", poll.id)}>
    <span class="answer-info">{poll.answerA}</span>
    <span class="answer-info total-votes">({poll.votesA})</span>
    <div class="percent-fill" style="width: {percentA}%"></div>
  </div>

  <div class="answer-b votes" on:keydown={() => {}} on:click={() => addVote("b", poll.id)}>
    <span class="answer-info">{poll.answerB}</span>
    <span class="answer-info total-votes">({poll.votesB})</span>
    <div class="percent-fill" style="width: {percentB}%"></div>
  </div>

  {#if totalVotes > 0}
    <p class="votes-total">Total votes: {totalVotes}</p>
  {:else}
    <p class="votes-total">No votes yet</p>
  {/if}
</div>

<style>
  .votes {
    background-color: rgb(247, 247, 247);

    position: relative;

    padding: 1rem;
    margin: 0.5rem 0;

    border-radius: 1rem;

    cursor: pointer;
    user-select: none;

    display: flex;
    justify-content: space-between;

    transition: 150ms ease-in-out;

    font-weight: bold;
  }

  .votes:hover {
    background-color: rgba(0, 0, 0, 0.05);
    transform: translateY(-5%);
  }

  .votes:active {
    transform: translateY(0);
  }

  .answer-info {
    z-index: 10;
  }

  .total-votes {
    font-style: italic;
    color: #aaa;
  }

  .percent-fill {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;

    transition: 250ms ease-in-out;

    border-radius: 1rem;
    background-color: rgb(233, 233, 233);
  }

  .votes-total {
    color: #bbb;
  }
</style>
