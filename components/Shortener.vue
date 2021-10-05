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
        src="/bg-shorten-desktop.svg"
        alt="just a bg image"
        class="shortener__bg-image"
      />
    </div>
  </div>
</template>

<script>
import { nanoid } from 'nanoid'

export default {
  data: () => ({
    link: '',
    error: '',
  }),
  methods: {
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
  }

  &__bg-image {
    display: block;

    position: absolute;
    z-index: -1;

    width: 100%;
    height: 100%;

    border-radius: 0.5rem;
  }
}
</style>
