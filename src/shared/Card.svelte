<!-- MARK: Logic
-->
<script>
</script>

<!-- MARK: Content
-->
<div class="card">
  <slot name="title"></slot>
  <slot name="details"></slot>
</div>

<!-- MARK: Styles
-->
<style>
  .card {
    border-radius: 1rem;

    padding: 1rem;
    margin: 1rem;

    box-shadow: 0 2px 0.25rem 0.1rem rgba(0, 0, 0, 0.1);

    position: relative;
  }
</style>
