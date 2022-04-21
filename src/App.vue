<template>
  <QuoteForm />
</template>

<script>
import QuoteForm from './components/quote-form.vue'

export default {
  name: 'App',
  components: {
    QuoteForm
  }
}
</script>

<style lang="scss">
:root {
  --primary: #1b105d;
  --secondary: #4099e0;
  --tertiary: #f06530;
}

body {
  margin: 0;
  font-size: .875rem;

  @media (min-width: 768px) {
    font-size: 1rem;
  }
}

h1, h2 {
  color: var(--primary);
  margin: 0;
  margin-bottom: .75rem;

  span {
    color: var(--secondary);
  }
}

h2 {
  font-size: 1.125rem;
  font-weight: 300;
}

#app {
  position: relative;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  font-family: sans-serif;

  @media(min-width: 768px) {
    align-items: center;
  }

  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 50%;
    background: var(--secondary);
    z-index: -1;
  }
}

input[type="radio"] {
  display: grid;
  place-content: center;
  appearance: none;
  background-color: #fff;
  margin: 0;
  font: inherit;
  color: currentColor;
  width: 1.75em;
  height: 1.75em;
  border: 0.15em solid var(--secondary);
  border-radius: 50%;
}

input[type="radio"]::before {
  content: "";
  width: 1.05em;
  height: 1.05em;
  border-radius: 50%;
  transform: scale(0);
  transition: 120ms transform ease-in-out;
  box-shadow: inset 1em 1em var(--secondary);
}

input[type="radio"]:checked::before {
  transform: scale(1);
}

.grid-span-1 {
  grid-column: span 2;

  @media(min-width: 768px) {
    grid-column: span 1;
  }
}

.grid-span-2 {
  grid-column: span 2;
}

.button {
  padding: 1rem 2rem;
  border-radius: 100px;
  background: var(--tertiary);
  border: none;
  color: white;
  font-size: 1.125rem;
  cursor: pointer;
  transition: all ease .2s;

  &:hover,
  &:focus-visible {
    background: var(--secondary);
  }

  &--disabled {
    cursor: not-allowed;
    opacity: .5;
  }
}
</style>
