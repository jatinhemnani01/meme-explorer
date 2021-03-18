<script>
  import { showAboutModal } from "../store/showAboutModalStore";
  import { fade } from "svelte/transition";
</script>

{#if $showAboutModal}
  <div
    height="100vh"
    on:click={() => {
      $showAboutModal = false;
    }}
    transition:fade={{ duration: 500 }}
  >
    <h2>Modal Example</h2>

    <!-- Trigger/Open The Modal -->
    <button id="myBtn">Open Modal</button>

    <!-- The Modal -->
    <div id="myModal" class="modal">
      <!-- Modal content -->
      <div class="modal-content">
        <span
          class="close"
          on:click={() => {
            $showAboutModal = false;
          }}>&times;</span
        >
        <p>
          I'm Jatin Hemnani the developer of this Website i.e .com. I enjoy
          memes and every time I have used to use Reddit for memes but the
          performance of Reddit was decreasing idk why and there are lot's of
          people who uses Reddit for meme content. So I created this website
          which let's you consume Reddit memes for free and it's very fast and
          Mobile Friendly. <strong
            >If you like to donate click on Donate and it will be very helpful
            to upgrade and give you new features.</strong
          >
        </p>
      </div>
    </div>
  </div>
{/if}

<style>
  /* The Modal (background) */
  .modal {
    /* Hidden by default */
    position: fixed; /* Stay in place */
    z-index: 1; /* Sit on top */
    padding-top: 100px; /* Location of the box */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgb(0, 0, 0); /* Fallback color */
    background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
  }

  /* Modal Content */
  .modal-content {
    background-color: #fefefe;
    margin: auto;
    padding: 20px;
    border: 1px solid #888;
    width: 80%;
  }

  /* The Close Button */
  .close {
    color: #aaaaaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
  }

  .close:hover,
  .close:focus {
    color: #000;
    text-decoration: none;
    cursor: pointer;
  }
</style>
