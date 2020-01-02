<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let todo = {
    title: "",
    completed: false
  };

  function handleSubmit() {
    if (todo.title !== "") {
      dispatch("add-todo", todo);
      todo.title = "";
    }
  }
</script>

<style>
  div {
    margin-top: 20px;
  }

  form {
    display: flex;
    align-items: center;
  }

  input {
    flex: 1;
    margin-right: 10px;
  }

  button {
    background-color: #fa8c16;
    color: white;
    border: none;
  }
</style>

<div>
  <form on:submit|preventDefault={handleSubmit}>
    <input
      bind:value={todo.title}
      type="text"
      name="todo"
      placeholder="Type something here..." />
    <button type="submit">+ Add</button>
  </form>
</div>
