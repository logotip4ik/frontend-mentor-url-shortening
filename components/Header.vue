<template>
  <header class="header">
    <div class="header__content">
      <h1 class="header__content__heading">More than just shorter links</h1>
      <p class="header__content__info">
        Build your own brand's recognition and get detailed insights on how your
        links are performing
      </p>
      <button class="btn btn--lg">Get Started</button>
    </div>
    <img
      src="/illustration-working.svg"
      alt="just a bg image"
      class="header__image"
    />
  </header>
</template>

<script>
export default {}
</script>

<style lang="scss">
.header {
  @include base-width;

  display: grid;
  align-items: center;
  grid-template-columns: 60% auto;
  gap: 1rem;

  padding-block: 2rem;

  &__content {
    max-width: 45ch;
    width: 100%;

    &__heading {
      font-size: 3.75rem;
      font-weight: 700;
      letter-spacing: -1px;
      line-height: 1.125;

      color: var(--neutral-very-dark-blue);
    }
    &__info {
      font-size: 1rem;
      color: var(--neutral-grayish-violet);

      margin-bottom: 2rem;
    }
  }
  &__image {
    display: block;
  }
}
</style>
