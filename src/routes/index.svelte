<script>
  let todos = [];

  let task = "";

  const addTodo = () => {
    let todo = {
      task: task,
      isComplete: false,
      createdAt: new Date()
    };
    todos = [todo, ...todos];
    task=""
  };

  const markTodoAsComplete = (index) => {
    todos[index].isComplete = !todos[index].isComplete
  }

  const deleteTodo = (index) => {
    let deleteItem = todos[index]
    todos = todos.filter((item) => item !=deleteItem)
  };

  $: console.table(todos)
</script>

<input type="text" placeholder="Add a task" bind:value={task}>
<button on:click={addTodo}>Add</button>

<ol>
 {#each todos as item, index}
    <li class:complete={item.isComplete}>
      <span>
        {item.task}
      </span>
      <span>
        <button on:click={() => markTodoAsComplete(index)}>✔</button>
        <button on:click={() => deleteTodo(index)}>✘</button>
      </span>
    </li>
    {:else}
    <p>No todos found</p>
 {/each}
</ol>

<style>
  .complete {
    text-decoration: line-through;
  }
</style>