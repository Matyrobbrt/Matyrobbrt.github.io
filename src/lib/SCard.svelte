<script>
  import { Card, CardBody, CardImg, CardText, CardTitle } from "sveltestrap";
  import { currentPageTheme } from "../routes/__layout.svelte";

  export let href = undefined;
  export let src = undefined;
  export let title = undefined;
  export let text = undefined;
  export let id = undefined;
  export let alt = undefined;
  export let cardClass = "card";
  export let bodyClass = "card_body";
  export let titleClass = "card_title";
  export let textClass = "card_text";

  let theme;
  currentPageTheme.subscribe(value => theme = value);
  let imgcss = `border-top-left-radius:20px;
  border-top-right-radius:20px;
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;`;
  let bodycss =
    "border-bottom-left-radius:20px;border-bottom-right-radius:20px;";
</script>

<Card class={cardClass + theme === "light" ? "bg-light" : "bg-dark"} {id} style="border-radius:20px;">
  <a {href} target="_blank">
    <img {src} {alt} style={imgcss}>
    <!-- <CardImg top {src} {alt} style={imgcss} /> -->

    <CardBody class={bodyClass} style={bodycss}>
      {#if title}
        <CardTitle class={titleClass}>{title}</CardTitle>
      {/if}
      {#if text != null}
        <CardText class={textClass}>{text}</CardText>
      {/if}
    </CardBody>
  </a>
</Card>

<style>
  :global(.card a) {
    text-decoration: none;
  }
  :global(.card_body) {
    background-color: black;
  }
  :global(.card_title) {
    font-size: 90%;
    text-align: center;
  }
  :global(.card.bg-dark a) {
    color: white;
  }
  :global(.bg-dark.card) {
    background-color: #121212;
  }
  :global(.card:hover) {
    transform: scale(1.015);
  }
  :global(.card) {
    margin: 15px;
    border-radius: 5px;
    -webkit-transition-duration: 0.25s;
    transition-duration: 0.15s;
  }
</style>
