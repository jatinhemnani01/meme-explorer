<script>
  import Card from "./components/Card.svelte";
  import { loading } from "./store/loadingStore";
  import { memes } from "./store/memesStore";
  import { inputSubreddit } from "./store/subredditStore";
  import { onMount } from "svelte";
  import Loading from "./components/Loading.svelte";
  import InputSubreddit from "./components/InputSubreddit.svelte";
  import ScrollToTop from "./components/ScrollToTop.svelte";
  import AboutModal from "./components/AboutModal.svelte";
  import Error from "./components/Error.svelte";
  import ContactModal from "./components/ContactModal.svelte";
  // function to fetch the memes
  async function getMemes(subreddit) {
    try {
      $loading = true;
      let res = await fetch(
        `https://meme-api.herokuapp.com/gimme/${subreddit}/5`
      );
      let data = await res.json();
      $memes = [...$memes, ...data.memes];
      $loading = false;
    } catch (error) {
      $loading = true;
    }
  }

  // function for infinite scrolling
  function loadMoreHandler() {
    window.addEventListener("scroll", () => {
      const {
        scrollTop,
        scrollHeight,
        clientHeight,
      } = document.documentElement;

      if (clientHeight + scrollTop >= scrollHeight - 150) {
        getMemes($inputSubreddit);
      }
    });
  }

  // onMount to fetch on start
  onMount(() => {
    getMemes($inputSubreddit);

    loadMoreHandler();
  });
</script>

<div class="main" id="middle">
  <!-- NAVBAR + FORM + SEARCH -->
  <InputSubreddit />

  <!-- SHOWS ERROR IF SUBREDDIT DOESN'T EXIST -->
  <Error />
  <!-- MAIN CARD -->
  <div class="main-card">
    <!-- SCROLL TO TOP BUTTON -->
    <ScrollToTop />

    <!-- LOOPING TO ALL MEMES -->
    {#each $memes as meme}
      <Card
        img_url={meme.preview[2]}
        title={meme.title}
        subreddit={meme.subreddit}
      />
    {:else}
      <!-- LOADING SCREEN -->
      <Loading />
    {/each}
  </div>
  {#if $loading}
    <!-- LOADING SPINNER -->
    <Loading />
  {/if}
  <AboutModal />

  <!-- CONTACT PAGE -->
  <ContactModal />
</div>

<style>
  .main {
    background-color: #2d3436;
  }
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
