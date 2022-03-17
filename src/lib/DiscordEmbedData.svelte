<script>
  export let url = "";
  export let description = "";
  export let image = "";
  export let colour = "#ffffff";
</script>

<head>
  <meta property="og:url" content={url} />
  <meta property="og:description" content={description} />
  <meta property="og:image" content={image} />
  <meta name="theme-color" content={colour} />
</head>