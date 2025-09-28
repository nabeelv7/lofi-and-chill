<script>
  import { onMount } from "svelte";
  import MusicPlayer from "./MusicPlayer.svelte";
  import ThemeControllers from "./ThemeControllers.svelte";
  import Options from "./Options.svelte";

  let pfpLink = $state("/pfps/male.png");
  let name = $state("Homo Sapien");

  // country
  let country = $state("Berlin");
  let flag = $state("🇩🇪");

  onMount(async () => {
    gender = localStorage.getItem("gender") || "male";
    name = localStorage.getItem("name") || "Homo Sapien";

    if (gender == "male") {
      pfpLink = "/pfps/male.png";
    } else {
      pfpLink = "/pfps/female.png";
    }

    const res = await fetch("https://ipwho.is");
    const data = await res.json();
    country = data.country;
    flag = data.flag.emoji;
  });
</script>

<div
  class="fixed bg-base-100 flex flex-col text-base-content top-5 left-5 border border-base-content/30 rounded-xl p-5 min-w-100"
>
  <!-- profile section -->
  <div class="flex justify-between items-center">
    <div class="flex gap-3 justify-start items-center">
      <img
        class="w-15 h-15 rounded-full ring ring-base-300 shadow-sm"
        src={pfpLink}
        alt="PFP"
      />
      <div class="flex flex-col">
        <h1 class="text-xl font-medium">
          {name}
        </h1>
        <p class="opacity-80">{flag} {country}</p>
      </div>
    </div>

    <!-- options -->
    <Options />
  </div>

  <MusicPlayer />
</div>

{#snippet ReloadIcon()}
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="24"
    height="24"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="lucide lucide-refresh-cw-icon lucide-refresh-cw"
    ><path d="M3 12a9 9 0 0 1 9-9 9.75 9.75 0 0 1 6.74 2.74L21 8" /><path
      d="M21 3v5h-5"
    /><path d="M21 12a9 9 0 0 1-9 9 9.75 9.75 0 0 1-6.74-2.74L3 16" /><path
      d="M8 16H3v5"
    /></svg
  >
{/snippet}
