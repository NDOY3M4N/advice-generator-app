<script lang="ts">
  import ButtonIcon from "./lib/ButtonIcon.svelte";
  import DividerIcon from "./lib/DividerIcon.svelte";

  let loading: boolean;

  interface IAdvice {
    id: number;
    advice: string;
  }

  function sleep(ms: number = 2000) {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }

  async function loadAdvice(): Promise<IAdvice> {
    loading = true;
    const res = await fetch("https://api.adviceslip.com/advice");

    // NOTE: sleep of 3s here for animation purposes 😊
    await sleep();

    if (!res.ok)
      throw new Error("Something went wrong. Please try again later");

    const data = await res.json();
    loading = false;

    return data.slip as IAdvice;
  }

  let promise = loadAdvice();

  function handleClick() {
    promise = loadAdvice();
  }
</script>

<main class="card">
  <!-- PERF: animate the height of the card on new advice -->
  {#await promise}
    Loading...
  {:then data}
    <h2 class="card__title">Advice #{data.id}</h2>
    <!-- FIX: There are some weird symbols not being UTF8-ed -->
    <q class="card__content">{data.advice}</q>
  {:catch error}
    <p>{error.message}</p>
  {/await}
  <div class="card__divide">
    <DividerIcon />
  </div>
  <div class="card__action">
    <button
      disabled={loading}
      on:click={handleClick}
      aria-label="Generate new advice"
      type="button"
      class:loading
    >
      <ButtonIcon />
    </button>
  </div>
</main>

<style>
  .card {
    position: relative;
    background-color: var(--card-color);
    padding: 2rem 1rem;
    border-radius: 10px;
  }

  .card__title {
    line-height: 1;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 2.5px;
    margin: 0;
    margin-block-end: 1rem;
    color: var(--accent-color);
  }

  .card__content {
    font-size: 1.5rem;
  }

  .card__divide {
    margin-block: 1.5rem;
    position: relative;
  }

  .card__divide::before,
  .card__divide::after {
    content: "";
    position: absolute;
    top: 10px;
    width: calc(50% - 1.5rem);
    height: 1px;
    background-color: var(--divider-color);
  }

  .card__divide::before {
    left: 0;
  }
  .card__divide::after {
    right: 0;
  }

  .card__action {
    position: absolute;
    inset-inline: 0;
    bottom: 0;
    transform: translateY(50%);
  }

  .card__action button {
    background-color: var(--accent-color);
    border-radius: 50%;
    padding: 1.2rem;
    display: inline-flex;
    align-items: center;
    justify-content: center;
  }

  .loading {
    animation: rotate 6s infinite linear;
  }

  @media (prefers-reduced-motion) {
    .loading {
      animation: none;
    }
  }

  @keyframes rotate {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }

  @media (min-width: 800px) {
    .card {
      padding: 3rem 4rem;
    }

    .card__title {
      font-size: 0.75rem;
    }

    .card__content {
      font-size: 1.75rem;
    }
  }
</style>
