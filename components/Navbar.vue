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
    <div class="nav__burger" @click="isNavActive = !isNavActive">
      <span class="nav__burger__line"></span>
      <span class="nav__burger__line"></span>
      <span class="nav__burger__line"></span>
    </div>
    <!-- COMMENT: i know,  it could be a lot better, but i am too lazy to refactor it D_D -->
    <div
      :class="{
        nav__wrapper: true,
        'nav__wrapper--mobile': true,
        'nav__wrapper--active': isNavActive,
      }"
    >
      <ul class="nav__list nav__list--mobile">
        <li class="nav__list__item" @click="isNavActive = false">Features</li>
        <li class="nav__list__item" @click="isNavActive = false">Pricing</li>
        <li class="nav__list__item" @click="isNavActive = false">Resources</li>
      </ul>
      <hr />
      <button class="btn btn--outlined" @click="isNavActive = false">
        Login
      </button>
      <button class="btn" @click="isNavActive = false">Sign Up</button>
    </div>
    <div class="nav__wrapper">
      <button class="btn btn--outlined">Login</button>
      <button class="btn">Sign Up</button>
    </div>
  </nav>
</template>

<script>
export default {
  data: () => ({
    isNavActive: false,
  }),
}
</script>

<style lang="scss">
.nav {
  @include base-width;
  display: flex;
  justify-content: space-between;
  align-items: center;

  position: relative;

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

    &--mobile {
      display: none;
      flex-direction: column;
      gap: 1rem;

      position: absolute;
      left: 50%;
      top: 100%;
      z-index: 10;

      width: 95vw;

      padding: 1.5rem 2rem;
      border-radius: 0.5rem;
      background-color: var(--primary-dark-violet);

      transform: translate(-50%, -150%);
      transition: transform 0.4s ease;

      .btn {
        font-size: 1rem;
        width: 100%;

        &--outlined {
          color: white;
        }
      }

      hr {
        width: 100%;
        opacity: 0.25;
      }
    }
    &--active {
      transform: translate(-50%, 0);
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

    &--mobile {
      width: 100%;
      flex-direction: column;

      .nav__list__item {
        color: white;
        font-size: 1rem;
        width: 100%;

        text-align: center;

        &:hover {
          color: var(--neutral-gray);
        }
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
    &__burger {
      display: flex;
    }
    &__wrapper {
      &:first-child .nav__list {
        display: none;
      }
      &:last-child {
        display: none;
      }
      &--mobile {
        display: flex;
      }
    }
  }
}
</style>
