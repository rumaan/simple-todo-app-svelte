<script>
  import Todos from "./components/Todos.svelte";
  import AddTodo from "./components/AddTodo.svelte";

  let todos = [];

  function toggleTodo(event) {
    const id = event.detail;
    todos = todos.map(todo => {
      if (todo.id === id) {
        todo.completed = !todo.completed;
      }
      return todo;
    });
  }

  function deleteTodo(event) {
    const id = event.detail;
    todos = todos.filter(todo => todo.id !== id);
  }

  function addTodo(event) {
    const todo = event.detail;
    todos = [...todos, { ...todo, id: todos.length + 1 }];
  }
</script>

<style>
  @import url("https://fonts.googleapis.com/css?family=Overpass:400,600&display=swap");

  :global(*) {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: "Overpass", sans-serif;
    -webkit-font-smoothing: subpixel-antialiased;
    -moz-font-smoothing: subpixel-antialiased;
  }

  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: #fafafa;
    min-height: 100vh;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  .card {
    min-width: 300px;
    max-width: calc(30% + 10vw);
    border-radius: 4px;
    padding: 1em;
    background: white;
    box-shadow: 0px 4px 12px rgba(0.1, 0.1, 0.1, 0.08);
  }

  .divider {
    width: 100%;
    border-bottom: 1px solid rgba(0.5, 0.5, 0.5, 0.1);
    margin: 14px 0;
  }

  h3,
  h5 {
    text-align: center;
  }
</style>

<main>
  <div class="card">
    <h3>
      Yet Another Todo App
      <span aria-label="Todo app icon">📚</span>
    </h3>
    <AddTodo on:add-todo={addTodo} />
    <div class="divider" />
    {#if todos.length === 0}
      <h5>No Todos here yet!</h5>
    {/if}
    <Todos {todos} on:toggle-todo={toggleTodo} on:delete-todo={deleteTodo} />
  </div>
</main>
