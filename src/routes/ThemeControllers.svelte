<script>
  import ThemeSwitcher from "./ThemeSwitcher.svelte";
</script>

<div>
  <span class="dark:hidden inline-flex">
    <ThemeSwitcher theme="dracula-mod" />
  </span>
  <span class="hidden dark:inline-flex">
    <ThemeSwitcher theme="garden-mod" />
  </span>
</div>
