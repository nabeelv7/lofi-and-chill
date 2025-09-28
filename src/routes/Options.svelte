<script>
  import shareds from "./shareds.svelte";
  import ThemeControllers from "./ThemeControllers.svelte";
</script>

<div class="dropdown dropdown-end">
  <div tabindex="0" role="button" class="m-1 cursor-pointer active:scale-95">
    {@render OptionsIcon()}
  </div>
  <ul
    class="dropdown-content border border-base-content/20 bg-base-200 rounded-box z-1 w-52 p-5 shadow-sm flex flex-col gap-2"
  >
    <li class="flex w-full justify-between">
      <p class="dark:hidden inline-flex">Dark Mode</p>
      <p class="dark:inline-flex hidden">Light Mode</p>
      <ThemeControllers />
    </li>
    <li class="mt-1">
      <button
        onclick={() => shareds.modal.showModal()}
        class="btn btn-primary w-full btn-sm"
        >{@render SettingsIcon()} Account Settings</button
      >
    </li>
  </ul>
</div>

{#snippet OptionsIcon()}
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
    class="lucide lucide-ellipsis-vertical-icon lucide-ellipsis-vertical"
    ><circle cx="12" cy="12" r="1" /><circle cx="12" cy="5" r="1" /><circle
      cx="12"
      cy="19"
      r="1"
    /></svg
  >
{/snippet}

{#snippet SettingsIcon()}
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="15"
    height="15"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="lucide lucide-settings-icon lucide-settings"
    ><path
      d="M9.671 4.136a2.34 2.34 0 0 1 4.659 0 2.34 2.34 0 0 0 3.319 1.915 2.34 2.34 0 0 1 2.33 4.033 2.34 2.34 0 0 0 0 3.831 2.34 2.34 0 0 1-2.33 4.033 2.34 2.34 0 0 0-3.319 1.915 2.34 2.34 0 0 1-4.659 0 2.34 2.34 0 0 0-3.32-1.915 2.34 2.34 0 0 1-2.33-4.033 2.34 2.34 0 0 0 0-3.831A2.34 2.34 0 0 1 6.35 6.051a2.34 2.34 0 0 0 3.319-1.915"
    /><circle cx="12" cy="12" r="3" /></svg
  >
{/snippet}
