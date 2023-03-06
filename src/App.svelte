<script lang="ts">
  interface Advice {
    id: number;
    advice: string;
  }

  async function getAdvice(): Promise<Advice> {
    const res = await fetch("https://api.adviceslip.com/advise");

    if (!res.ok)
      throw new Error("Something went wrong. Please try again later");

    const data = await res.json();
    return data.slip as Advice;
  }

  // TODO: should I do this onMount lifecycle hook?
  // TODO: choose a better name
  let promise = getAdvice();

  // PERF: disable the button for 2 seconds (the API will send the same advice if you don't wait for 2 seconds)
  function handleClick() {
    promise = getAdvice();
  }
</script>

<main>
  <!-- PERF: smooth animation of the card on a new advice -->
  <section class="card">
    {#await promise}
      <!-- PERF: use a spinner here maybe -->
      ...waiting
    {:then data}
      <h2 class="card__title">Advice #{data.id}</h2>
      <q class="card__content">{@html data.advice}</q>
    {:catch error}
      <p>{error.message}</p>
    {/await}
    <div class="card__divide">
      <svg width="295" height="16" xmlns="http://www.w3.org/2000/svg">
        <g transform="translate(138)" fill="#CEE3E9">
          <rect width="6" height="16" rx="3" />
          <rect x="14" width="6" height="16" rx="3" />
        </g>
      </svg>
    </div>
    <div class="card__action">
      <button on:click={handleClick} aria-label="Generate new advice">
        <svg width="24" height="24" xmlns="http://www.w3.org/2000/svg"
          ><path
            d="M20 0H4a4.005 4.005 0 0 0-4 4v16a4.005 4.005 0 0 0 4 4h16a4.005 4.005 0 0 0 4-4V4a4.005 4.005 0 0 0-4-4ZM7.5 18a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Z"
            fill="#202733"
          /></svg
        >
      </button>
    </div>
  </section>
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
    /* TODO: use rem values here / change the size on desktop */
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 2.5px;
    margin: 0;
    margin-block-end: 1rem;
    color: var(--accent-color);
  }

  .card__content {
    /* TODO: use rem / on desktop it is 28px */
    font-size: 24px;
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
</style>
