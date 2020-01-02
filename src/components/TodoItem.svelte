<script>
  import { createEventDispatcher } from "svelte";
  import { fade, fly } from "svelte/transition";

  const dispatch = createEventDispatcher();

  export let todo;
</script>

<style>
  .todo-item {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    cursor: pointer;
    padding: 4px 0px;
    min-height: 45px;
  }

  .todo-item:hover {
    background-color: rgba(0.1, 0.1, 0.1, 0.025);
    border-radius: 4px;
  }

  .todo-item div {
    flex: 1;
    display: flex;
    align-items: center;
  }

  p {
    margin-left: 12px;
    font-size: 0.95em;
    font-weight: 500;
  }

  .delete {
    margin-left: 1em;
    font-size: 0.8em;
  }

  .completed {
    text-decoration: line-through;
    color: grey;
  }
</style>

<div
  class="todo-item"
  in:fly={{ y: 20, duration: 400 }}
  out:fly={{ x: 20, duration: 400 }}>
  <div on:click={() => dispatch('toggle-todo', todo.id)}>
    {#if todo.completed}
      <span
        aria-label="Task Complete Thumb icon"
        transition:fly={{ y: 5, duration: 200 }}>
        👍
      </span>
    {/if}
    <p class={todo.completed ? 'completed' : ''}>{todo.title}</p>
  </div>
  <span
    class="delete"
    aria-label="Delete Todo Icon"
    on:click={() => dispatch('delete-todo', todo.id)}>
    🗑
  </span>
</div>
