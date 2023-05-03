<script>
  import Total from "./Total.svelte";

  let newItem = "";

  let todoList = [
    { text: "Write my first post", status: true },
    { text: "Upload the post to the blog", status: false },
    { text: "Publish the post at Facebook", status: false },
  ];

  function addToList() {
    todoList = [...todoList, { text: newItem, status: false }];
    newItem = "";
  }

  function removeFromList(index) {
    todoList.splice(index, 1);
    todoList = todoList;
  }

  $: total = todoList.length;
  $: {
    console.log("total:", total);
  }
</script>

<Total {total} />

<input bind:value={newItem} type="text" placeholder="new todo item.." />
<button on:click={addToList}>Add</button>
{#if total >= 3}
  <div>🐷</div>
{/if}

<br />
{#each todoList as item, index}
  <input bind:checked={item.status} type="checkbox" />
  <span class:checked={item.status}>{item.text}</span>
  <span on:click={() => removeFromList(index)}>❌</span>
  <br />
{/each}

<style>
  .checked {
    text-decoration: line-through;
  }
</style>
