<script>
  export let poll = {};

  const addVote = (option) => {
    let optionToEdit = Object.keys(poll).filter((key) => {
      return key === `votes${option.toUpperCase()}`;
    });

    poll[optionToEdit] = ++poll[optionToEdit];
    console.log((poll.votesA / 100) * totalVotes);
  };

  $: totalVotes = poll.votesA + poll.votesB;

  $: percentA = Math.floor((100 / totalVotes) * poll.votesA);
  $: percentB = Math.floor((100 / totalVotes) * poll.votesB);

  console.log(totalVotes);
</script>

<div>
  <div class="answer-a votes" on:keydown={() => {}} on:click={() => addVote("a", poll.id)}>
    <span class="answer-info">{poll.answerA}</span>
    <span class="answer-info">({poll.votesA})</span>
    <div class="percent-fill" style="width: {percentA}%"></div>
  </div>

  <div class="answer-b votes" on:keydown={() => {}} on:click={() => addVote("b", poll.id)}>
    <span class="answer-info">{poll.answerB}</span>
    <span class="answer-info">({poll.votesB})</span>
    <div class="percent-fill" style="width: {percentB}%"></div>
  </div>

  <p>Total votes: {totalVotes}</p>
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
  }

  .votes:hover {
    background-color: rgba(0, 0, 0, 0.05);
  }

  .votes:active {
    transform: translateY(5%);
  }

  .answer-info {
    z-index: 10;
  }

  .percent-fill {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;

    transition: 100ms ease-in-out;

    border-radius: 1rem;
    background-color: rgb(255, 196, 208);
  }
</style>
