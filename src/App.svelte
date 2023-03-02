<main>
  <section class="card">
    <h2 class="card__title">Advice #117</h2>
    <p class="card__content">
      "It is easy to sit pu and take notice, what's difficult is getting up and
      taking action."
    </p>
    <div class="card__divide">
      <svg width="295" height="16" xmlns="http://www.w3.org/2000/svg"
        ><g fill="none" fill-rule="evenodd"
          ><path fill="#4F5D74" d="M0 8h122v1H0zM173 8h122v1H173z" /><g
            transform="translate(138)"
            fill="#CEE3E9"
            ><rect width="6" height="16" rx="3" /><rect
              x="14"
              width="6"
              height="16"
              rx="3"
            /></g
          ></g
        ></svg
      >
    </div>
    <div class="card__action">
      <button aria-label="Generate new advice">
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
    background-color: hsl(217, 19%, 24%);
    /* TODO: find a better padding solution */
    padding: 2rem 1rem 2.5rem;
    border-radius: 5px;
  }

  .card__title {
    line-height: 1;
    font-size: 0.8rem;
    text-transform: uppercase;
    letter-spacing: 2.5px;
    font-weight: 500;
    margin: 0;
    color: hsl(150, 100%, 66%);
  }

  .card__content {
    margin-block-start: 1rem;
    font-weight: 600;
    color: hsl(193, 38%, 86%);
  }

  .card__divide {
    margin-block-start: 1.5rem;
  }

  .card__action {
    position: absolute;
    inset-inline: 0;
    bottom: 0;
    transform: translateY(50%);
  }
</style>

