<script>
  import ImageModal from "./ImageModal.svelte";
  import { showModal } from "../store/showModalStore";
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
<div class="ui card card-container">
  <div class="image">
    <img
      on:click={() => {
        $showModal = true;
      }}
      src={img_url}
      alt={title}
    />
  </div>
  <div class="content">
    <div class="header">{title}</div>
  </div>
  <div class="extra content">
    <div>
      <i class="user icon" />
      {subreddit}
    </div>
  </div>
</div>

<style>
  .card-container {
    cursor: pointer;
    background-color: #6b4242;
  }
</style>
