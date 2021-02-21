<script>
  import Card from "./components/Card.svelte";
  import { onMount } from "svelte";
  import Loading from "./components/Loading.svelte";
  let memes = [];
  let loading = false;
  async function getMemes() {
    try {
      loading = true;
      let res = await fetch("https://meme-api.herokuapp.com/gimme/dankmemes/5");
      let data = await res.json();
      memes = [...memes, ...data.memes];
      loading = false;
    } catch (error) {}
  }

  onMount(() => {
    getMemes();
  });
  window.addEventListener("scroll", () => {
    const { scrollTop, scrollHeight, clientHeight } = document.documentElement;

    if (clientHeight + scrollTop >= scrollHeight - 150) {
      getMemes();
    }
  });
</script>

<div>
  <div class="main-card">
    {#each memes as meme}
      <Card
        img_url={meme.preview[2]}
        title={meme.title}
        subreddit={meme.subreddit}
      />
    {:else}
      <Loading />
    {/each}
  </div>
  {#if loading}
    <Loading />
  {/if}
</div>

<style>
  .main-card {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    justify-items: center;
    padding: 2em;
    background-color: #2d3436;
  }
  @media screen and (max-width: 350px) {
    .main-card {
      padding: 0px;
    }
  }
</style>
