<script>
  import { onMount } from "svelte";

  let index = $state(0);
  let isPlaying = $state(false);
  let progress = $state(0);
  let playButton = $state();
  let audioEl;

  let songs = [
    { name: "Main Rahun", singer: "Samar Jafri", link: "/main-rahun.mp3" },
    { name: "Zaalima", singer: "Abdul Hannan", link: "/zaalima.mp3" },
    {
      name: "Kehdena",
      singer: "Annural Khalid",
      link: "/kehdena.mp3",
    },
  ];

  function togglePlay() {
    if (!audioEl) return;
    if (isPlaying) {
      audioEl.pause();
      isPlaying = false;
    } else {
      audioEl.play();
      isPlaying = true;
    }
  }

  function nextSong() {
    index = (index + 1) % songs.length;
    loadAndPlay();
  }

  function prevSong() {
    index = (index - 1 + songs.length) % songs.length;
    loadAndPlay();
  }

  async function loadAndPlay() {
    if (!audioEl) return;
    audioEl.src = songs[index].link;
    audioEl.load();
    try {
      await audioEl.play();
      isPlaying = true;
    } catch (err) {
      isPlaying = false; // play blocked (e.g. no user interaction)
    }
  }

  onMount(() => {
    if (audioEl) {
      audioEl.src = songs[index].link;
    }
  });

  function updateProgress() {
    if (!audioEl || !audioEl.duration) return;
    progress = (audioEl.currentTime / audioEl.duration) * 100;
  }

  function seek(e) {
    if (!audioEl || !audioEl.duration) return;
    const newTime = (e.target.value / 100) * audioEl.duration;
    audioEl.currentTime = newTime;
  }
</script>

<div class="flex justify-between items-center gap-10 rounded-box max-w-md">
  <!-- metadata -->
  <div class="mb-4">
    <h1 class="text-xl font-semibold">{songs[index].name}</h1>
    <p class="opacity-80">{songs[index].singer}</p>
  </div>

  <!-- controls -->
  <div class="flex flex-col justify-center gap-4 mt-4">
    <!-- progress -->
    <input
      type="range"
      min="0"
      max="100"
      value={progress}
      class="range range-xs range-primary"
      oninput={seek}
    />
    <!-- buttons -->
    <div class="flex items-center justify-between">
      <button class="btn btn-circle" onclick={prevSong}
        >{@render PlayPrevious()}</button
      >
      <button
        bind:this={playButton}
        class="btn btn-circle btn-primary flex justify-center items-center"
        onclick={togglePlay}
      >
        {#if isPlaying}
          {@render PauseIcon()}
        {:else}
          {@render PlayIcon()}
        {/if}
      </button>
      <button class="btn btn-circle" onclick={nextSong}
        >{@render PlayNext()}</button
      >
    </div>
  </div>

  <!-- hidden audio element -->
  <audio bind:this={audioEl} ontimeupdate={updateProgress} onended={nextSong}
  ></audio>
</div>

{#snippet PauseIcon()}
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="24"
    height="24"
    viewBox="0 0 24 24"
    fill="currentColor"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="lucide lucide-pause-icon lucide-pause"
    ><rect x="14" y="3" width="5" height="18" rx="1" /><rect
      x="5"
      y="3"
      width="5"
      height="18"
      rx="1"
    /></svg
  >
{/snippet}

{#snippet PlayIcon()}
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="24"
    height="24"
    viewBox="0 0 24 24"
    fill="currentColor"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="lucide lucide-play-icon lucide-play"
    ><path
      d="M5 5a2 2 0 0 1 3.008-1.728l11.997 6.998a2 2 0 0 1 .003 3.458l-12 7A2 2 0 0 1 5 19z"
    /></svg
  >
{/snippet}

{#snippet PlayNext()}
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="24"
    height="24"
    viewBox="0 0 24 24"
    fill="currentColor"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="lucide lucide-skip-forward-icon lucide-skip-forward"
    ><path d="M21 4v16" /><path
      d="M6.029 4.285A2 2 0 0 0 3 6v12a2 2 0 0 0 3.029 1.715l9.997-5.998a2 2 0 0 0 .003-3.432z"
    /></svg
  >
{/snippet}

{#snippet PlayPrevious()}
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="24"
    height="24"
    viewBox="0 0 24 24"
    fill="currentColor"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="lucide lucide-skip-back-icon lucide-skip-back"
    ><path
      d="M17.971 4.285A2 2 0 0 1 21 6v12a2 2 0 0 1-3.029 1.715l-9.997-5.998a2 2 0 0 1-.003-3.432z"
    /><path d="M3 20V4" /></svg
  >
{/snippet}
