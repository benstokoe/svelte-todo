<script>
  export let numberOfTasks;
</script>

<style>

</style>

<footer class="footer">
  <div class="content has-text-centered">
    <p>{numberOfTasks} remaining todo{#if numberOfTasks === 0}s{/if}</p>
  </div>
</footer>
