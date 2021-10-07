<template>
  <div class="booster">
    <h4 class="booster__header">Boost your links today</h4>
    <button class="btn btn--xlg">Get Started</button>
    <img
      srcset="/bg-boost-desktop.svg 9999999w, /bg-boost-mobile.svg 600w"
      alt="just a bg pattern"
      class="booster__bg-image"
    />
  </div>
</template>

<style lang="scss">
.booster {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 1.5rem;

  position: relative;
  isolation: isolate;

  width: 100%;
  padding: 3.5rem 2rem;
  background-color: var(--primary-dark-violet);

  &__header {
    font-size: 2.125rem;
    font-size: clamp(1.25rem, 5vw, 2.125rem);
    text-align: center;

    color: white;
  }

  &__bg-image {
    position: absolute;
    z-index: -1;
    inset: 0;

    width: 100%;
    height: 100%;
  }
}
</style>
