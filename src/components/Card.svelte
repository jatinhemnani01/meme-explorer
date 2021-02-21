<script>
  import { fade } from "svelte/transition";
  export let img_url;
  export let title;
  export let subreddit;
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/components/card.min.css"
    integrity="sha512-u5E5vOHVsB0blcZniDNfaRkTfqdgjxIgLX17YlG0vjQyos7Z7b1BXLuhHZbF2JOVRrfNNd8P6v7fw87JaFw/Rg=="
    crossorigin="anonymous"
  />
</svelte:head>
<div class="ui card card-container" transition:fade={{ duration: 400 }}>
  <div class="image">
    <img src={img_url} alt={title} />
  </div>
  <div class="content">
    <div class="header">{title}</div>
  </div>
  <div class="extra content">
    <div class="badge">
      <i class="user icon " />
      r/{subreddit}
    </div>
  </div>
</div>

<style>
  .badge {
    width: 42%;
    background-color: #636e72;
    color: #dfe6e9;
    border-radius: 106px;
    text-align: center;
    padding: 0.1em;
  }
  .card-container {
    display: flex;
    justify-content: center;
    width: 100%;
  }
</style>
