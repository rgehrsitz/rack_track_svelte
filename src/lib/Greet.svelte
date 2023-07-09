<script lang="ts">
  import { invoke } from "@tauri-apps/api/tauri";
  import { Button } from "flowbite-svelte";

  let name = "";
  let greetMsg = "";

  async function greet() {
    // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
    greetMsg = await invoke("greet", { name });
  }
</script>

<div>
  <form class="row" on:submit|preventDefault={greet}>
    <input id="greet-input" placeholder="Enter a name..." bind:value={name} />
    <Button type="submit" color="blue">Greet</Button>
  </form>
  <p>{greetMsg}</p>
</div>
