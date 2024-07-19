<script>
  import { createEventDispatcher } from 'svelte';

  export let tabs;
  export let activeTab;

  const dispatch = createEventDispatcher();

  function handleAddTab() {
    dispatch('addTab');
  }

  function handleRenameTab(id) {
    const newName = prompt('Enter new tab name:');
    if (newName) {
      dispatch('renameTab', { id, name: newName });
    }
  }

  function switchTab(id) {
    dispatch('switchTab', id);
  }
</script>

<nav>
  <ul>
    {#each tabs as tab}
      <li class:active={tab.id === activeTab}>
        <button on:click={() => switchTab(tab.id)}>{tab.name}</button>
        <button class="rename-btn" on:click={() => handleRenameTab(tab.id)}>✏️</button>
      </li>
    {/each}
  </ul>
  <button class="add-tab" on:click={handleAddTab}>+ Add Tab</button>
</nav>

<style>
  nav {
    background-color: #1e1e1e;
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-wrap: wrap;
  }

  li {
    margin-right: 10px;
    margin-bottom: 5px;
    display: flex;
    align-items: center;
  }

  button {
    background-color: #333;
    color: white;
    border: none;
    padding: 10px 15px;
    cursor: pointer;
    border-radius: 5px;
  }

  .active button {
    background-color: #555;
  }

  .add-tab {
    background-color: #4CAF50;
  }

  .rename-btn {
    background: none;
    border: none;
    color: white;
    cursor: pointer;
    font-size: 0.8em;
    padding: 5px;
    margin-left: 5px;
  }

  @media (max-width: 600px) {
    nav {
      flex-direction: column;
    }

    ul {
      margin-bottom: 10px;
    }
  }
</style>