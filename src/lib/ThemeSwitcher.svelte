<script>
  import { currentPageTheme } from "../routes/__layout.svelte";
  import { onMount } from "svelte";
  const STORAGE_KEY = "theme";
  const DARK_PREFERENCE = "(prefers-color-scheme: dark)";
  const THEMES = {
    DARK: "dark",
    LIGHT: "light",
  };
  let currentTheme;
  currentPageTheme.subscribe((value) => (currentTheme = value));
  const prefersDarkThemes = () => window.matchMedia(DARK_PREFERENCE).matches;
  export function applyTheme() {
    const preferredTheme = prefersDarkThemes() ? THEMES.DARK : THEMES.LIGHT;
    currentTheme = localStorage.getItem(STORAGE_KEY) ?? preferredTheme;
    currentPageTheme.set(currentTheme);
    if (currentTheme === THEMES.DARK) {
      document.body.classList.remove(THEMES.LIGHT);
      document.body.classList.add(THEMES.DARK);
      checked = true;
    } else {
      document.body.classList.remove(THEMES.DARK);
      document.body.classList.add(THEMES.LIGHT);
      checked = false;
    }
    return "";
  }
  function toggleTheme() {
    const stored = localStorage.getItem(STORAGE_KEY);
    if (stored) {
      localStorage.removeItem(STORAGE_KEY);
    } else {
      localStorage.setItem(
        STORAGE_KEY,
        prefersDarkThemes() ? THEMES.LIGHT : THEMES.DARK
      );
    }
    applyTheme();
    switchCardColour();
  }
  export function switchCardColour() {
    var elements = document.getElementsByClassName("card");
    Array.from(elements).forEach((element) => {
      if (currentTheme === THEMES.DARK) {
        element.classList.toggle("bg-light", false);
        element.classList.toggle("bg-dark", true);
      } else {
        element.classList.toggle("bg-light", true);
        element.classList.toggle("bg-dark", false);
      }
    });
    return "";
  }
  let checked = true;
  const uniqueID = Math.floor(Math.random() * 100);
  function handleClick(event) {
    const target = event.target;
    const state = target.getAttribute("aria-checked");
    checked = state === "true" ? false : true;
    toggleTheme();
  }
  onMount(async () => {
    applyTheme();
    window.matchMedia(DARK_PREFERENCE).addEventListener("change", applyTheme);
  });
</script>

<div class="s--switcher" style="font-size:20px">
  <span id={`switch-${uniqueID}`}>Dark Theme</span>
  <button
    role="switch"
    aria-checked={checked}
    aria-labelledby={`switch-${uniqueID}`}
    on:click={handleClick}
  />
</div>

<style>
  :root {
    --accent-color: CornflowerBlue;
    --gray: #ccc;
  }

  .s--switcher {
    display: flex;
    align-items: center;
    float: right;
    margin-top: 1rem;
    margin-bottom: 1rem;
  }
  .s--switcher button {
    width: 3em;
    height: 1.6em;
    position: relative;
    margin: 0 0 0 0.5em;
    background: var(--gray);
    border: none;
  }
  .s--switcher button::before {
    content: "";
    position: absolute;
    width: 1.3em;
    height: 1.3em;
    background: #fff;
    top: 0.13em;
    right: 1.5em;
    transition: transform 0.3s;
  }
  .s--switcher button[aria-checked="true"] {
    background-color: var(--accent-color);
  }
  .s--switcher button[aria-checked="true"]::before {
    transform: translateX(1.3em);
    transition: transform 0.3s;
  }
  .s--switcher button:focus {
    box-shadow: 0 0px 0px 1px var(--accent-color);
  }
  .s--switcher button {
    border-radius: 1.5em;
  }
  .s--switcher button::before {
    border-radius: 100%;
  }
  .s--switcher button:focus {
    box-shadow: 0 0px 8px var(--accent-color);
    border-radius: 1.5em;
  }
</style>
