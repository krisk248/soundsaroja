<script>
	import { onMount } from 'svelte';
	import Navbar from './components/Navbar.svelte';
	import Tab from './components/Tab.svelte';
  
	let tabs = [{ id: 1, name: 'Tab 1', sounds: [] }];
	let activeTab = 1;
  
	function addTab() {
	  const newTabId = tabs.length + 1;
	  tabs = [...tabs, { id: newTabId, name: `Tab ${newTabId}`, sounds: [] }];
	  activeTab = newTabId;
	}
  
	function addSounds(tabId, newSounds) {
	  tabs = tabs.map(tab => {
		if (tab.id === tabId) {
		  return { ...tab, sounds: [...tab.sounds, ...newSounds] };
		}
		return tab;
	  });
	}
  
	function renameTab(tabId, newName) {
	  tabs = tabs.map(tab => {
		if (tab.id === tabId) {
		  return { ...tab, name: newName };
		}
		return tab;
	  });
	}
  
	onMount(() => {
	  document.body.classList.add('dark-mode');
	});
  </script>
  
  <main>
	<h1>Sound saroja</h1>
	<Navbar {tabs} {activeTab} on:addTab={addTab} on:renameTab={(event) => renameTab(event.detail.id, event.detail.name)} on:switchTab={(event) => activeTab = event.detail} />
	
	{#each tabs as tab (tab.id)}
	  {#if tab.id === activeTab}
		<Tab {tab} on:addSounds={(event) => addSounds(tab.id, event.detail)} />
	  {/if}
	{/each}
  </main>
  
  <style>
	:global(body) {
	  margin: 0;
	  padding: 0;
	  font-family: Arial, sans-serif;
	}
  
	:global(.dark-mode) {
	  background-color: #121212;
	  color: #ffffff;
	}
  
	main {
	  padding: 20px;
	  max-width: 1200px;
	  margin: 0 auto;
	}
  </style>