<script>
  import { isError } from "../store/errorStore";
  import { fly } from "svelte/transition";
</script>

{#if $isError}
  <div
    in:fly={{ duration: 400, y: 300 }}
    out:fly={{ duration: 300, y: -200 }}
    id="snackbar"
  >
    Subreddit Doesn't Exist
  </div>
{/if}

<style>
  #snackbar {
    visibility: visible;
    min-width: 250px;
    background-color: #e03838;
    color: #fff;
    text-align: center;
    border-radius: 2px;
    padding: 16px;
    z-index: 1;
    bottom: 30px;
    font-size: 17px;
  }

  @-webkit-keyframes fadein {
    from {
      bottom: 0;
      opacity: 0;
    }
    to {
      bottom: 30px;
      opacity: 1;
    }
  }

  @keyframes fadein {
    from {
      bottom: 0;
      opacity: 0;
    }
    to {
      bottom: 30px;
      opacity: 1;
    }
  }

  @-webkit-keyframes fadeout {
    from {
      bottom: 30px;
      opacity: 1;
    }
    to {
      bottom: 0;
      opacity: 0;
    }
  }

  @keyframes fadeout {
    from {
      bottom: 30px;
      opacity: 1;
    }
    to {
      bottom: 0;
      opacity: 0;
    }
  }
</style>
