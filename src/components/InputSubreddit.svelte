<script>
  import { loading } from "../store/loadingStore";
  import { memes } from "../store/memesStore";
  import { inputSubreddit } from "../store/subredditStore";

  async function getSubredditMemes(subreddit) {
    try {
      $loading = true;
      let res = await fetch(
        `https://meme-api.herokuapp.com/gimme/${subreddit}/5`
      );
      let data = await res.json();
      $memes = $memes;
      $memes = [...$memes, ...data.memes];
      $loading = false;
    } catch (error) {
      $loading = true;
    }
  }
</script>

<form on:submit|preventDefault={() => getSubredditMemes($inputSubreddit)}>
  <input type="text" bind:value={$inputSubreddit} />
</form>
