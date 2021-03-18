<script>
  import { showContactModal } from "../store/showContactModal";
  import { fade } from "svelte/transition";
</script>

{#if $showContactModal}
  <div height="100vh" transition:fade={{ duration: 500 }}>
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
            $showContactModal = false;
          }}>&times;</span
        >
        <strong>Email:</strong> <br /><strong>jatinhemnani01@gmail.com</strong>
        <br />
        <strong
          ><a href="https://www.instagram.com/jatinhemnani1/" target="_blank"
            >Instagram</a
          ></strong
        >
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
