<template>
  <section class="quote-form">
    <div class="quote-form__top">
      <div class="quote-form__top-content">
        <h1>Compare <span>Life Insurance</span> Quotes</h1>
        <h2>Search the market for competitive life insurance quotes from <span>Legal &amp; General, Aviva, Zurich</span> &amp; more!</h2>
      </div>
    </div>
    <div class="quote-form__bottom">
      <form>
        <div class="quote-form__left">
          <div
            class="quote-form__input grid-span-1"
            :class="{ 'quote-form__input--error' : formErrors.includes(`firstName`) }"
          >
            <label>First Name</label>
            <input v-model="formData.firstName" type="text">
          </div>
          <div
            class="quote-form__input grid-span-1"
            :class="{ 'quote-form__input--error' : formErrors.includes(`lastName`) }"
          >
            <label>Last Name</label>
            <input v-model="formData.lastName" type="text">
          </div>
          <div
            class="quote-form__input grid-span-2"
            :class="{ 'quote-form__input--error' : formErrors.includes(`email`) }"
          >
            <label>Email</label>
            <input v-model="formData.email" type="email">
          </div>
        </div>
        <div class="quote-form__right">
          <label for="policy-radio">Who is this policy for?</label>
          <fieldset :class="{ 'error' : formErrors.includes(`policyChoice`) }" id="policy-radio">
            <label>
              <input v-model="formData.policyChoice" type="radio" name="policy-radio" value="Just myself">
              Just myself
            </label>
            <label>
              <input v-model="formData.policyChoice" type="radio" name="policy-radio" value="Me and My Partner">
              Me and My Partner
            </label>
          </fieldset>
          <button
            class="button"
            :class="{ 'button--disabled' : !formValidation }"
            :title="formValidation ? `Get my free quote` : `Please fill in the form`"
            @click="submitForm"
          >
            Get My Free Quote
          </button>
        </div>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      formData: {
        firstName: null,
        lastName: null,
        email: null,
        policyChoice: null,
      },
      formErrors: [],
    }
  },
  methods: {
    submitForm (e) {
      e.preventDefault()
      this.renderErrors()
      console.table(this.formData)
    },
    renderErrors () {
      //Create a list of form inputs which values are null or an empty string
      this.formErrors = Object.entries(this.formData)
        .filter(entry => entry[1] === null || entry[1] === ``)
        .map(item => item[0])
    }
  },
  computed: {
    formValidation () {
      //Check that every form input has a value (Controls submit button disabled class and title)
      return Object.values(this.formData).every(item => item)
    }
  }
};
</script>

<style lang="scss" scoped>
.quote-form {
  background: white;
  border-radius: 5px;
  padding: 2rem;
  box-shadow: 0 0 5px 0 rgba(0,0,0,.4);
  margin: .5rem;

  &__top {
    display: flex;
    justify-content: center;
    border-bottom: solid 1px lightgrey;
    margin-bottom: 1.5rem;
    padding-bottom: 1rem;

    &-content {
      max-width: 425px;
      text-align: center;
    }
  }

  &__bottom {
    
    form {
      display: flex;
      flex-direction: column;
      flex-wrap: nowrap;
      align-items: center;
      gap: 2rem;

      @media(min-width: 768px) {
        gap: 4rem;
        flex-direction: row;
        align-items: flex-start;
      }
    }
  }

  &__left {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    width: 100%;

    @media(min-width: 768px) {
      width: auto;
    }
  }

  &__right {
    display: flex;
    flex-direction: column;
    gap: .5rem;

    fieldset {
      display: flex;
      flex-direction: column;
      border: none;
      padding: .5rem;

      &.error {
        border: solid 2px red;
        border-radius: 5px;
      }

      label {
        display: flex;
        flex-wrap: nowrap;
        align-items: center;
        gap: .5rem;
        font-size: .9rem;
        margin-bottom: .5rem;
      }
    }
  }

  &__input {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: .5rem;
    width: 100%;

    input {
      width: 100%;
      box-sizing: border-box;
      padding: .5rem;
    }

    &--error {

      input {
        border: solid 2px red;
      }
    }
  }
}
</style>
