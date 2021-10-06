<template>
  <div class="statistics">
    <header class="statistics__header">
      <h3 class="statistics__header__heading">Advanced Statistics</h3>
      <p class="statistics__header__info">
        Track how your links are performing across the web with our advanced
        statistics dashboard.
      </p>
    </header>
    <ul class="statistics__articles">
      <li class="statistics__articles__article">
        <img
          src="/icon-brand-recognition.svg"
          alt="brand recognition icon"
          class="statistics__articles__article__icon"
        />
        <h4 class="statistics__articles__article__header">Brand Recognition</h4>
        <p class="statistics__articles__article__info">
          Boost your brand recognition with each click. Generic links don’t mean
          a thing. Branded links help instil confidence in your content.
        </p>
      </li>
      <li class="statistics__articles__article">
        <img
          src="/icon-detailed-records.svg"
          alt="detailed records icon"
          class="statistics__articles__article__icon"
        />
        <h4 class="statistics__articles__article__header">Detailed Records</h4>
        <p class="statistics__articles__article__info">
          Gain insights into who is clicking your links. Knowing when and where
          people engage with your content helps inform better decisions.
        </p>
      </li>
      <li class="statistics__articles__article">
        <img
          src="/icon-fully-customizable.svg"
          alt="fully customizable icon"
          class="statistics__articles__article__icon"
        />
        <h4 class="statistics__articles__article__header">
          Fully Customizable
        </h4>
        <p class="statistics__articles__article__info">
          Improve brand awareness and content discoverability through
          customizable links, supercharging audience engagement.
        </p>
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
.statistics {
  @include base-width;

  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
  gap: 2rem;

  position: relative;

  padding-block: 3rem;

  &__header {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex-direction: column;
    gap: 0.5rem;

    max-width: 37ch;
    text-align: center;

    &__heading {
      font-size: 2rem;
      color: var(--neutral-very-dark-blue);
    }
    &__info {
      font-size: 0.9rem;
      color: var(--neutral-grayish-violet);
    }
  }

  &__articles {
    display: flex;
    justify-content: space-between;
    justify-content: space-around;
    align-items: center;
    flex-wrap: wrap;
    gap: 2rem;

    position: relative;

    list-style-type: none;
    padding-block: 4rem;

    &__article {
      position: relative;

      max-width: 315px;
      border-radius: 0.25rem;
      padding: 3.5rem 1.5rem 2rem;
      background-color: white;

      // prettier-ignore
      box-shadow:
        0px 0.1px 2.2px rgba(0, 0, 0, 0.003),
        0px 0.3px 5.3px rgba(0, 0, 0, 0.004),
        0px 0.6px 10px rgba(0, 0, 0, 0.005),
        0px 1.1px 17.9px rgba(0, 0, 0, 0.006),
        0px 2.1px 33.4px rgba(0, 0, 0, 0.007),
        0px 5px 80px rgba(0, 0, 0, 0.01)
      ;

      &__icon {
        position: absolute;
        top: -2.25rem;

        padding: 1rem;
        border-radius: 100vmin;
        background-color: var(--primary-dark-violet);
      }
      &__header {
        font-size: 1.1rem;
        color: var(--neutral-very-dark-blue);
        margin-block-end: 1rem;
      }
      &__info {
        font-size: 0.75rem;
        color: var(--neutral-grayish-violet);
      }

      &:nth-child(1) {
        bottom: 2rem;
      }
      &:nth-child(3) {
        top: 2rem;
      }
    }

    &::after {
      content: '';

      position: absolute;
      z-index: -1;
      left: 50%;
      top: 50%;

      width: 90%;
      height: 4px;
      background-color: var(--primary-cyan);

      transform: translate(-50%, -50%);
    }
  }

  &::after {
    content: '';

    position: absolute;
    top: 0;
    left: 50%;
    z-index: -1;

    width: 100vw;
    height: 100%;
    background-color: #f7f7f7;
    transform: translate(-50%, 0);
  }
}
</style>
