<!-- MARK: Logic
-->
<script>
  export let useHeaderImg = false;
</script>

<!-- MARK: Content
-->
<div>
  {#if useHeaderImg}
    <img class="logo" src="/assets/logo.svg" alt="Poll Ninja" />
  {:else}
    <h2 class="title">Polls Ninja</h2>
  {/if}
</div>

<!-- MARK: Styles
-->
<style>
  div {
    display: flex;
    flex-direction: column;

    align-items: center;
    justify-content: center;

    background-color: #f7f7f7;
  }

  .title {
    font-size: 2rem;
    padding: 1rem;
  }

  .logo {
    width: 340px;
  }
</style>
