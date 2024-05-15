<!-- MARK: Logic
-->
<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let isPrimary = true;

  export let buttonText = "OK";

  let isHovered = false;

  const changeHoverStatus = () => {
    isHovered = !isHovered
  }
</script>


<!-- MARK: Content
-->
<div>
  <button class={isPrimary ? 'primary' : 'secondary'} class:inverse={isHovered}
    on:mouseenter={changeHoverStatus}
    on:mouseleave={changeHoverStatus}
    on:click={() => dispatch('onButtonClick')}>
    {buttonText}
  </button>
</div>


<!-- MARK: Styles
-->
<style>
  button {
    padding: 0.25rem 1rem;

    border: none;
    border-radius: 0.5rem;

    font-weight: bold;

    cursor: pointer;
    user-select: none;
  }

  button:active {
    transform: translateY(2%);
  }

  .primary {
    border: 2px solid  #f7f7f7;
    background-color: #dc143c;
    color: #f7f7f7;
  }
  .secondary {
    border: 2px solid  #f7f7f7;
    background-color: #4169e1;
    color: #f7f7f7;
  }

  .primary.inverse {
    border: 2px solid  #dc143c;
    background-color: #f7f7f7;
    color:  #dc143c;
  }
  .secondary.inverse {
    border: 2px solid #4169e1;
    background-color: #f7f7f7;
    color: #4169e1;
  }
</style>