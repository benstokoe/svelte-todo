<script>
  import { Field, Input, Button } from "svelma";

  import Todo from "./Todo.svelte";
  import Actions from "./Actions.svelte";

  let todos = [
    {
      id: 1,
      task: "Get milk",
      completed: false
    }
  ];
  let newTodo = "";

  const addTodo = () => {
    const todo = {
      id: todos.length ? todos[todos.length - 1].id + 1 : 1,
      task: newTodo,
      completed: false
    };

    todos = [todo, ...todos];

    newTodo = "";
  };

  const deleteTodo = id => {
    todos = todos.filter(todo => todo.id !== id);
  };

  const completeTodo = todo => {
    const index = todos.findIndex(({ id }) => id === todo.id);

    const newTodo = {
      ...todo,
      completed: !todo.completed
    };

    todos = [...todos.slice(0, index), newTodo, ...todos.slice(index + 1)];
  };

  $: tasksToBeCompleted = todos.filter(todo => !todo.completed).length;
</script>

<style>
  .container {
    text-align: center;
  }

  .todos {
    margin: 30px;
  }
</style>

<section class="hero is-primary">
  <div class="hero-body">
    <div class="container">
      <h1 class="title">Let's Do These Things</h1>

      <form on:submit|preventDefault={addTodo}>
        <Input
          type="text"
          class="is-rounded"
          id="todo"
          placeholder="Add Todo"
          size="is-large"
          bind:value={newTodo} />
      </form>
    </div>
  </div>
</section>

<div class="todos">
  <ul class="container">
    {#each todos as todo}
      <Todo
        {...todo}
        deleteTodo={() => deleteTodo(todo.id)}
        completeTodo={() => completeTodo(todo)} />
    {/each}
  </ul>
</div>

<Actions numberOfTasks={tasksToBeCompleted} />
