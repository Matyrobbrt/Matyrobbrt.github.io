<script context="module">
  import { writable } from "svelte/store";
  export async function httpGet(url, callback) {
    fetch(url)
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        callback(data);
      })
      .catch(console.log);
  }
  export const currentPageTheme = writable("dark");
</script>

<slot />

<style>
  :global(.container) {
    max-width: 1140px;
  }
  :global(body.light) {
    background-color: azure;
    color: black;
  }
  :global(body.dark) {
    background-color: #020616;
    color: white;
  }
</style>
