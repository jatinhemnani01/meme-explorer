<script>
  import Card from "./components/Card.svelte";
  import { showModal } from "./store/showModalStore";
  import { onMount } from "svelte";
  import ImageModal from "./components/ImageModal.svelte";
  let memes = [];
  async function getMemes() {
    try {
      let res = await fetch("https://meme-api.herokuapp.com/gimme/dankmemes/5");
      let data = await res.json();
      memes = [...memes, ...data.memes];
    } catch (error) {}
  }

  onMount(() => {
    getMemes();
  });
</script>

<div>
  {#each memes as meme}
    <ImageModal img_url={meme.url} title={meme.title} />
    <Card img_url={meme.url} title={meme.title} subreddit={meme.subreddit} />
  {:else}
    <h2>Loading....</h2>
  {/each}
</div>
