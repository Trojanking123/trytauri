<script>
  import { invoke } from "@tauri-apps/api/core";
  import { open } from "@tauri-apps/plugin-dialog";

  let name = "";
  let greetMsg = "";
  let save_dir = "";

  async function greet() {
    greetMsg = await invoke("greet", { name });
  }

  async function choose_dir() {
    save_dir = await open({
      multiple: false,
      directory: true,
    });
    
  }
</script>

<div>
  
  <form class="column" on:submit|preventDefault={greet}>
    <input id="greet-input" placeholder="Enter a name..." bind:value={name} />
    <br>
    
    <input id="greet-input" placeholder="Enter a dir..." bind:value={save_dir} />
    <button  on:click={choose_dir}>choose your directory</button>
    <br>
    <button type="submit"> </button>
  </form>
  <p>{greetMsg}</p>
</div>
