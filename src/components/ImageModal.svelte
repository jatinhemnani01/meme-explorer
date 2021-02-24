<script>
  import { showModal } from "../store/showModalStore";
  import { fade } from "svelte/transition";
</script>

{#if $showModal}
  <div transition:fade={{ duration: 500 }} class="modal-wrapper">
    <span
      class="close"
      on:click={() => {
        $showModal = false;
      }}>&times;</span
    >
    <div
      class="modal"
      on:click|self={() => {
        $showModal = false;
      }}
    >
      <div class="donate">Click On Below Button To Donate</div>
      <br />
      <form>
        <script
          src="https://checkout.razorpay.com/v1/payment-button.js"
          data-payment_button_id="pl_GfQFdLtveYUasE"
          async>
        </script>
      </form>
      <div class="thanks">Thank You For Your Generous Donations</div>
    </div>
  </div>
{/if}

<style>
  .thanks {
    color: black;
    background: #b5cc18;
    padding: 1em;
    font-size: 1.6em;
  }
  form {
    padding: 1em;
  }
  .donate {
    background-color: green;
    padding: 1em;
    color: white;
    font-size: 1.5em;
  }
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
    flex-direction: column;
  }
  .close {
    float: right;
    color: white;
    padding: 1em;
    cursor: pointer;
    font-size: 25px;
  }
</style>
