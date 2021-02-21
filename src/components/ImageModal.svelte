<script>
  import { showModal } from "../store/showModalStore";
  import { fade } from "svelte/transition";
  export let title;
  export let img_url;
</script>

{#if $showModal}
  <div transition:fade={{ duration: 500 }} class="modal-wrapper">
    <span
      class="close"
      on:click={() => {
        $showModal = false;
      }}>&times;</span
    >
    <div class="modal">
      <img src={img_url} alt={title} />
    </div>
  </div>
{/if}

<style>
  .modal-wrapper {
    background-color: rgba(0, 0, 0, 0.6);
    position: fixed;
    width: 100%;
    height: 100vh;
    top: 0;
    left: 0;
  }
  .modal {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
  }
  img {
    width: 100%;
    object-fit: contain;
    height: 90vh;
  }
  .close {
    float: right;
    color: white;
    padding: 1em;
    cursor: pointer;
    font-size: 25px;
  }
</style>
