<script>
  import { loading } from "../store/loadingStore";
  import { memes } from "../store/memesStore";
  import { inputSubreddit } from "../store/subredditStore";
  import { showAboutModal } from "../store/showAboutModalStore";
  async function getSubredditMemes(subreddit) {
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
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/components/menu.min.css"
    integrity="sha512-ox96Q1iqhM5TvdY4gVbz6FXoDwsR/Q8jq15kWReQNefC+uUGCv+pkMbLOtr176K3+bfrQQv6gTDAvhL1PUw2YQ=="
    crossorigin="anonymous"
  />
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/components/icon.min.css"
    integrity="sha512-8Tb+T7SKUFQWOPIQCaLDWWe1K/SY8hvHl7brOH8Nz5z1VT8fnf8B+9neoUzmFY3OzkWMMs3OjrwZALgB1oXFBg=="
    crossorigin="anonymous"
  />
</svelte:head>

<div class="ui pointing menu" id="myForm">
  <div class="active item">Explore</div>
  <div
    class="item"
    on:click={() => {
      $showAboutModal = true;
      console.log("ww");
    }}
  >
    About
  </div>
  <a href="https://rzp.io/l/AieLJo1rd" target="_blank" class="item">Donate</a>
  <div class="right menu custom" id="right">
    <div class="item" id="items">
      <div class="ui transparent icon input">
        <form
          on:submit|preventDefault={() => getSubredditMemes($inputSubreddit)}
        >
          <strong>r/</strong><input
            required
            type="text"
            placeholder="Search Subreddit"
            on:input={(e) => ($inputSubreddit = e.target.value)}
          />
          <i
            on:click={() => getSubredditMemes($inputSubreddit)}
            class="search link icon"
          />
        </form>
      </div>
    </div>
  </div>
</div>
<div class="ui segment">
  <p />
</div>

<style>
  @media screen and (max-width: 430px) {
    #myForm {
      display: flex;
      flex-direction: column;
      width: 100%;
      justify-content: center;
      text-align: center;
      align-items: center;
    }
    #right {
      margin-left: 0px !important;
    }
  }

  input {
    font-size: 1.4em;
  }
  strong {
    font-size: 1.8em;
    margin: 0.2em;
  }
</style>
