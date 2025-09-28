<script>
  import MusicPlayer from "./MusicPlayer.svelte";
  import ThemeSwitcher from "./ThemeSwitcher.svelte";
</script>

<div
  class="fixed bg-base-100 flex flex-col text-base-content top-5 left-5 border border-base-content/30 rounded-xl p-5 min-w-100"
>
  <!-- profile section -->
  <div class="flex justify-between items-center">
    <div class="flex gap-3 justify-start items-center">
      <img
        class="w-15 h-15 rounded-full ring ring-base-300 shadow-sm"
        src="/48.png"
        alt="PFP"
      />
      <div class="flex flex-col">
        <h1 class="text-xl font-medium">Nabeel Sadiq</h1>
        <p class="opacity-80">Germany 🇩🇪</p>
      </div>
    </div>

    <!-- theme switcher -->
    <div>
      <span class="dark:hidden inline-flex">
        <ThemeSwitcher theme="dracula-mod" />
      </span>
      <span class="hidden dark:inline-flex">
        <ThemeSwitcher theme="garden-mod" />
      </span>
    </div>
  </div>

  <MusicPlayer />
</div>
