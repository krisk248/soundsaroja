<script>
  import { createEventDispatcher } from 'svelte';
  import SoundBox from './SoundBox.svelte';

  export let tab;

  const dispatch = createEventDispatcher();

  function handleFileSelect(event) {
    const files = Array.from(event.target.files);
    const newSounds = files.map(file => ({
      name: file.name,
      url: URL.createObjectURL(file)
    }));
    dispatch('addSounds', newSounds);
  }
</script>

<div class="tab-content">
  <div class="sound-grid">
    {#each tab.sounds as sound (sound.url)}
      <SoundBox {sound} />
    {/each}
  </div>
  <div class="add-sound-container">
    <input
      type="file"
      id="sound-input-{tab.id}"
      accept="audio/*"
      multiple
      on:change={handleFileSelect}
      style="display: none;"
    />
    <label for="sound-input-{tab.id}" class="add-sound-button">+ Add Sound</label>
  </div>
</div>

<style>
  .tab-content {
    margin-top: 20px;
  }

  .sound-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 20px;
    margin-bottom: 20px;
  }

  .add-sound-container {
    text-align: center;
  }

  .add-sound-button {
    background-color: #4CAF50;
    color: white;
    padding: 10px 15px;
    cursor: pointer;
    border-radius: 5px;
    display: inline-block;
  }
</style>