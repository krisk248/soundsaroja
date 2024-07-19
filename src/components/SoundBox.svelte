<script>
  import { onDestroy } from 'svelte';

  export let sound;

  let audio;
  let isPlaying = false;

  function togglePlay() {
    if (isPlaying) {
      audio.pause();
      audio.currentTime = 0;
    } else {
      audio.play();
    }
    isPlaying = !isPlaying;
  }

  onDestroy(() => {
    if (audio) {
      audio.pause();
      audio.src = '';
    }
  });
</script>

<div class="sound-box" class:playing={isPlaying} on:click={togglePlay}>
  <p>{sound.name}</p>
  <audio bind:this={audio} src={sound.url} preload="none"></audio>
</div>

<style>
  .sound-box {
    background-color: #333;
    border-radius: 5px;
    padding: 15px;
    text-align: center;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .sound-box:hover {
    background-color: #444;
  }

  .playing {
    background-color: #4CAF50;
  }

  p {
    margin: 0;
    word-break: break-word;
  }
</style>