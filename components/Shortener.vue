<template>
  <div class="shortener__wrapper">
    <div class="shortener">
      <div class="shortener__input-wrapper">
        <input
          v-model="link"
          type="text"
          placeholder="Shorten a link here..."
          :class="{ shortener__input: true, 'shortener__input--error': error }"
          @keypress.enter.prevent="shortenLink"
          @blur="error = ''"
        />
        <transition name="fade" mode="out-in">
          <span v-if="error === 'no-link'" key="1" class="shortener__error">
            Please add a link
          </span>
          <span
            v-else-if="error === 'not-a-link'"
            key="2"
            class="shortener__error"
          >
            Please add a valid link
          </span>
        </transition>
      </div>
      <button class="btn shortener__button" @click="shortenLink">
        Shorten It!
      </button>
      <img
        srcset="/bg-shorten-desktop.svg, /bg-shorten-mobile.svg 825w"
        alt="just a bg image"
        class="shortener__bg-image"
      />
    </div>

    <transition-group
      name="list"
      class="shortener__links"
      mode="out-in"
      tag="ul"
    >
      <li
        v-for="linkObj in links"
        :key="linkObj.id"
        class="shortener__links__link"
      >
        <h2 class="shortener__links__link__header">{{ linkObj.link }}</h2>
        <p class="shortener__links__link__shorten">{{ linkObj.shortenLink }}</p>
        <button
          class="btn shortener__links__link__copy-button"
          @click="() => copyLink(linkObj.shortenLink)"
        >
          Copy
          <!-- [ ] add copied text and animation for it -->
        </button>
      </li>
    </transition-group>
  </div>
</template>

<script>
import { nanoid } from 'nanoid'
import copy from 'copy-to-clipboard'

export default {
  props: { links: { type: Array, required: true, default: () => [] } },
  data: () => ({
    link: '',
    error: '',
  }),
  methods: {
    copyLink(link) {
      copy(link, {
        format: 'text/plain',
        onCopy: () => this.$toast.success('Copied!'),
      })
    },
    shortenLink() {
      if (!this.link) return (this.error = 'no-link')
      if (!this.link.match(/(ftp|https?):\/\/[^ "]+$/))
        return (this.error = 'not-a-link')
      this.error = ''

      const { protocol, host } = window.location
      const hostname = `${protocol}//${host}`
      const shortenLinkId = nanoid(5)
      const shortenLink = {
        id: shortenLinkId,
        link: this.link,
        shortenLink: `${hostname}/${shortenLinkId}`,
      }

      this.$emit('create-link', shortenLink)
      this.link = ''
    },
  },
}
</script>

<style lang="scss">
.shortener__wrapper {
  @include base-width;

  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: stretch;
  gap: 1rem;

  position: relative;

  &::after {
    content: '';
    position: absolute;
    z-index: -1;
    top: 0;
    left: 50%;
    height: 100%;
    width: 100vw;

    transform: translate(-50vw, 30%);
    background-color: #f7f7f7;
  }
}

.shortener {
  display: grid;
  grid-template-columns: 80% auto;
  gap: 1rem;

  position: relative;

  isolation: isolate;
  border-radius: 0.5rem;
  padding: 2rem 1.5rem;
  background-color: var(--primary-dark-violet);

  &__input-wrapper {
    position: relative;
    width: 100%;
  }

  &__input {
    font: inherit;
    font-size: 0.9rem;

    width: 100%;
    border: none;
    outline: 2px solid transparent;
    border-radius: 0.25rem;
    padding: 0.75rem 1rem;

    appearance: none;
    transition: outline-color 0.4s ease;

    &::placeholder {
      font-weight: 500;

      opacity: 0.5;
      color: black;

      transition: color 0.4s ease;
    }

    &--error {
      outline-color: var(--secondary-red);
      &::placeholder {
        color: var(--secondary-red);
      }
    }
  }

  &__error {
    position: absolute;
    top: calc(100% + 0.25rem);
    left: 0;

    font-size: 0.8rem;
    font-style: italic;
    color: var(--secondary-red);
  }

  &__button {
    border-radius: 0.5rem;
    padding-block: 0.75rem;

    &::after {
      border-radius: 0.5rem;
    }
  }

  &__bg-image {
    display: block;

    position: absolute;
    z-index: -1;
    left: 0;
    top: 0;

    width: 100%;
    height: 100%;

    border-radius: 0.5rem;
  }

  &__links {
    display: flex;
    justify-content: center;
    align-items: stretch;
    flex-direction: column;
    gap: 1rem;

    position: relative;

    &__link {
      display: grid;
      align-items: center;
      grid-template-columns: 50% auto 5rem;
      gap: 1rem;

      background-color: white;
      border-radius: 0.5rem;
      padding: 0.75rem 1rem;
      // prettier-ignore
      box-shadow:
        0px 0.1px 2.2px rgba(0, 0, 0, 0.003),
        0px 0.3px 5.3px rgba(0, 0, 0, 0.004),
        0px 0.6px 10px rgba(0, 0, 0, 0.005),
        0px 1.1px 17.9px rgba(0, 0, 0, 0.006),
        0px 2.1px 33.4px rgba(0, 0, 0, 0.007),
        0px 5px 80px rgba(0, 0, 0, 0.01)
      ;

      &__header {
        position: relative;

        font-size: 1rem;
        font-weight: 500;
        color: var(--neutral-very-dark-blue);

        user-select: all;

        &::after {
          content: '';

          position: absolute;
          top: calc(100% + 0.45rem);
          left: 50%;

          opacity: 0;
          width: calc(100% + calc(1rem * 2));
          height: 2px;
          background-color: hsla(0, 0%, 75%, 0.25);

          transform: translateX(-50%);
        }
      }

      &__shorten {
        font-size: 0.9rem;
        color: var(--primary-cyan);

        justify-self: end;
        user-select: all;
      }

      &__copy-button {
        border-radius: 0.25rem;

        &::after {
          border-radius: 0.25rem;
        }
      }

      @media screen and (max-width: 825px) {
        display: flex;
        justify-content: flex-start;
        align-items: stretch;
        flex-direction: column;

        &__header::after {
          opacity: 1;
        }
      }
    }
  }

  @media screen and (max-width: 825px) {
    display: flex;
    justify-content: flex-start;
    align-items: stretch;
    flex-direction: column;
    gap: 2rem;
  }
}
</style>
