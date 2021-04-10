<script>
  import { loading } from "../store/loadingStore";
  import { memes } from "../store/memesStore";
  import { inputSubreddit } from "../store/subredditStore";
  import { isError } from "../store/errorStore";
  import { showContactModal } from "../store/showContactModal";
  import RoundBadge from "./RoundBadge.svelte";

  // function for fetching subreddit memes
  async function getSubredditMemes(subreddit) {
    $loading = true;
    let res = await fetch(
      `https://meme-api.herokuapp.com/gimme/${subreddit}/5`
    );
    if (res.ok) {
      let data = await res.json();
      $memes = data.memes;
      $loading = false;
      $isError = false;
    } else {
      $loading = true;
      $isError = true;
    }
  }
</script>

<!-- css frameworkds -->
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
  <div style="cursor:pointer;" class="active item">Explore</div>
  <div
    style="cursor:pointer;"
    class="item"
    on:click={() => {
      $showContactModal = true;
    }}
  >
    Contact
  </div>
  <!-- RAZORPAY -->
  <a
    rel="noopener noreferrer"
    href="https://rzp.io/l/XWshUz4"
    target="_blank"
    class="item">Donate</a
  >
  <!-- RAZORPAY -->
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
<RoundBadge />

<style>
  @media screen and (max-width: 570px) {
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
