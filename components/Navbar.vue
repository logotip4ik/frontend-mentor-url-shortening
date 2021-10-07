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
    <div class="nav__burger">
      <span class="nav__burger__line"></span>
      <span class="nav__burger__line"></span>
      <span class="nav__burger__line"></span>
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

  &__burger {
    --burger-gap: 0.35rem;

    display: none;
    flex-direction: column;
    justify-content: center;
    align-items: stretch;
    gap: var(--burger-gap);

    width: 30px;

    cursor: pointer;

    &__line {
      width: 100%;
      height: 3px;

      background-color: var(--neutral-grayish-violet);
      border-radius: 0.125rem;

      transition: background-color 0.4s ease;
    }

    &:hover &__line {
      background-color: var(--neutral-very-dark-blue);
      transition: none;
    }
  }

  @media screen and (max-width: 685px) {
    &__list {
      display: none;
    }
    &__burger {
      display: flex;
    }
    &__wrapper:last-child {
      display: none;
    }
  }
}
</style>
