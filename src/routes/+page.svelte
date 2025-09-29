<script>
  import { onMount } from "svelte";
  import MusicPlayerIsland from "./MusicPlayerIsland.svelte";
  import shareds from "./shareds.svelte";

  onMount(() => {
    if (
      !localStorage.getItem("signedIn") ||
      localStorage.getItem("signedIn") === "false"
    ) {
      shareds.modal.showModal();
    }
  });

  let name = $state();
  let gender = $state();

  function handleSubmit() {
    localStorage.setItem("name", name);
    localStorage.setItem("gender", gender);
    localStorage.setItem("signedIn", "true");
    window.location.reload();
  }
</script>

<MusicPlayerIsland />
<video width="100%" height="100%" src="/bg.mp4" loop autoplay muted></video>

<!-- sign up modal -->
<!-- <button class="btn" onclick="my_modal_2.showModal()">open modal</button> -->

<dialog bind:this={shareds.modal} id="signup-modal" class="modal">
  <div class="modal-box w-fit min-w-sm">
    <h3 class="text-2xl font-bold mb-5">👤 Account Settings</h3>

    <!-- form -->
    <p class="mb-2">What is your name?</p>
    <input
      bind:value={name}
      class="input rounded-md w-full"
      placeholder="Enter name here.."
      type="text"
    />

    <p class="mb-2 mt-5">What is your gender?</p>
    <select bind:value={gender} class="select w-full" name="gender" id="gender">
      <option value="male">Male</option>
      <option value="female">Female</option>
    </select>

    <button onclick={handleSubmit} class="btn btn-primary w-full mt-3"
      >Submit</button
    >
  </div>
  <form method="dialog" class="modal-backdrop">
    <button>close</button>
  </form>
</dialog>
