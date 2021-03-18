<script>
  import { inputSubreddit } from "../store/subredditStore";
  import { loading } from "../store/loadingStore";
  import { memes } from "../store/memesStore";
  import Spinner from "./Spinner.svelte";

  let badges = [
    { id: 1, sub: "memes" },
    { id: 2, sub: "dankinindia" },
    { id: 3, sub: "lol" },
    { id: 4, sub: "memeeconomy" },
    { id: 5, sub: "prequelmemes" },
    { id: 6, sub: "PewdiepieSubmissions" },
    { id: 7, sub: "blackpeopletwitter" },
    { id: 8, sub: "shittyadviceanimals" },
    { id: 9, sub: "wholesomememes" },
  ];

  async function getMemes(subreddit) {
    try {
      $loading = true;
      let res = await fetch(
        `https://meme-api.herokuapp.com/gimme/${subreddit}/5`
      );
      let data = await res.json();
      $memes = data.memes;
      $loading = false;
    } catch (error) {
      $loading = true;
    }
  }

  function handleBadge(sub) {
    $inputSubreddit = sub;
    getMemes(sub);
  }
</script>

<div class="badge-cont">
  {#each badges as badge (badge.id)}
    <div class="badge" on:click={() => handleBadge(badge.sub)}>
      r/{badge.sub}
    </div>
  {/each}
</div>
{#if $loading}
  <Spinner />
{/if}

<style>
  .badge-cont {
    width: 100%;
    display: flex;
    overflow-x: auto;
    white-space: nowrap;
  }
  .badge {
    margin-left: 10px;
    color: #d5d5d5;
    border: 1px solid #373737;
    padding: 7px;
    background-color: #555555;
    border-radius: 16px;
    cursor: pointer;
    transition: ease 0.2s;
  }
  .badge:hover {
    background-color: #424242;
  }
  .badge::after {
    background-color: #373737;
  }
</style>
