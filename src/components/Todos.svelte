<script>
  import TodoItem from "./TodoItem.svelte";

  export let todos;
</script>

<div>
  {#each todos as todo (todo.id)}
    <!-- Bubble Toggle Event up -->
    <TodoItem {todo} on:toggle-todo on:delete-todo/>
  {/each}
</div>
