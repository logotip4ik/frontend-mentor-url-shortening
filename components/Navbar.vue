<template>
  <nav class="nav">
    <div class="nav__wrapper">
      <img src="/logo.svg" alt="Shorlty Logo" class="nav__logo" />
      <ul class="nav__list">
        <li class="nav__list__item">Features</li>
        <li class="nav__list__item">Pricing</li>
        <li class="nav__list__item">Resources</li>
      </ul>
    </div>
    <div class="nav__wrapper">
      <button class="btn btn--outlined">Login</button>
      <button class="btn">Sign Up</button>
    </div>
  </nav>
</template>

<script>
export default {}
</script>

<style lang="scss">
.nav {
  @include base-width;
  display: flex;
  justify-content: space-between;
  align-items: center;

  padding-block: 2rem;

  &__wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1.25rem;

    &:first-child {
      justify-content: flex-start;
      gap: 2.5rem;
    }
    &:last-child {
      justify-content: flex-end;
    }
  }

  &__list {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 1.25rem;

    list-style-type: none;

    &__item {
      font-size: 0.75rem;
      color: var(--neutral-grayish-violet);

      cursor: pointer;
      transition: color 0.4s ease;

      &:hover {
        color: var(--primary-dark-violate);
        transition: none;
      }
    }
  }
}
</style>
