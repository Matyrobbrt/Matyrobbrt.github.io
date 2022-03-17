<script>
  import SCard from "$lib/SCard.svelte";
  import Footer from "$lib/Footer.svelte";
  import ThemeSwitcher from "$lib/ThemeSwitcher.svelte";
  import BootstrapImporter from "$lib/BootstrapImporter.svelte";
  import { CardGroup, Container } from "sveltestrap";
  import "../global.css";
  import "./__layout.svelte";
</script>

<head>
  <BootstrapImporter />
</head>

<Container>
  <main>
    <section id="links"  width="20%">
      <h2><a href="./#links" class="no-highlight">Links</a></h2>
      <br />
      <CardGroup>
        <SCard
          href="https://discord.gg/vV25kEaWJX"
          src="./assets/discord-logo.png"
          id="discord"
          alt="Discord logo"
          title="Discord - matyrobbrt#1756"
          cardClass="info_card"
        />
        <SCard
          href="https://www.github.com/Matyrobbrt"
          src="./assets/github.png"
          id="github"
          alt="Github logo"
          title="Github - Matyrobbrt"
          cardClass="info_card"
        />
        <SCard
          href="https://www.curseforge.com/members/matyrobbrt/projects"
          src="./assets/curse.png"
          id="curse_forge"
          alt="CurseForge logo"
          title="CurseForge - Matyrobbrt"
          cardClass="info_card"
        />
      </CardGroup>
    </section>
    <Footer />
    <ThemeSwitcher />
  </main>
</Container>

<style>
  :global(.info_card) {
    height: 60px;
    margin-top: 0;
    padding: 5px 10px 5px 10px;
  }
</style>
