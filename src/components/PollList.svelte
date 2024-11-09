<script>
  import PollDeatils from "./PollDeatils.svelte";

  export let polls = [];
</script>

<div class="container mt-5">
  <div class="row">
    {#each polls as poll}
      <div class="col-md-6 mb-4 fade-in">
        <PollDeatils {poll} on:vote/>
      </div>
    {/each}
  </div>
</div>

<style>
  .fade-in {
    opacity: 0;
    transform: translateY(30px);
    animation: fadeInUp 0.8s ease-in-out forwards;
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
</style>
