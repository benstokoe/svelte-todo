<script>
  import { Button } from "svelma";

  export let id;
  export let task;
  export let completed;
  export let completeTodo;
  export let deleteTodo;
</script>

<style>
  .todo {
    display: flex;
    justify-content: space-between;
  }

  .completed {
    text-decoration: line-through;
  }
</style>

<li class="todo" class:completed>
  <div>
    <input type="checkbox" checked={completed} on:click={completeTodo} />

    <span>{task}</span>
  </div>

  <Button on:click={deleteTodo}>Delete</Button>
</li>
