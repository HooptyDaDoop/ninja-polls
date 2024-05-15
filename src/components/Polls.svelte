<!-- MARK: Logic
-->
<script>
  import Card from "../shared/Card.svelte";
  import PollDetails from "./PollDetails.svelte";

  export let polls = [];
</script>

<!-- MARK: Content
-->
<div class="cards-wrapper">
  {#each polls as poll (poll.id)}
    <Card>
      <h2 slot="title">{poll.question}</h2>
      <PollDetails slot="details" {poll} on:vote on:polDelete></PollDetails>
    </Card>
  {/each}
</div>

<!-- MARK: Styles
-->
<style>
  .cards-wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr;

    margin: 2rem;
  }

  @media only screen and (max-width: 750px) {
    .cards-wrapper {
      grid-template-columns: 1fr;
    }
  }

  @media only screen and (min-width: 1920px) {
    .cards-wrapper {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
</style>
