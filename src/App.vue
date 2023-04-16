<template>
  <!-- Header -->
  <Header />

  <section class="container">
    <!-- Search Bar -->
    <form class="form" @submit.prevent>
      <div class="form__input">
        <input type="text" placeholder="Type your word here..." :value="word" @input="word = $event.target.value">
        <button class="search-btn" @click="sendRequest">
          <img src="./assets/search.png" alt="Search Icon">
        </button>
      </div>
    </form>

    <!-- Dictionary Viewer -->
    <DictionaryDisplay :data="data" />
  </section>
</template>

<script>
import Header from './components/Header.vue';
import DictionaryDisplay from './components/DictionaryDisplay.vue';

export default {
  data() {
    return {
      API: 'https://api.dictionaryapi.dev/api/v2/entries/en/',
      word: 'hello',
      data: ''
    }
  },
  created() {
    this.sendRequest();
  },
  components: {
    Header,
    DictionaryDisplay
  },
  methods: {
    async sendRequest() {
      const res = await fetch(this.API+this.word);
      let data  = await res.json();

      this.word = '';
      console.log(data);
      this.data = data[0];
    }
  }
}
</script>

<style lang="scss" scoped>
@use './scss/variables' as var;

// Search Bar
.form {
  padding: 50px 0;

  &__input {
    width: 100%;
    height: 70px;
    background: var.$clr-lt-grey;
    border-radius: 12px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 1px solid transparent;
    transition: all 0.3s;

    &:focus-within {
      border-color: var.$clr-accent-purple;
    }
    
    input {
      padding: 23px 30px;
      width: 100%;
      height: 100%;
      background: transparent;
      outline: none;
      border: none;
      font-size: var.$fs-txt-20;
      font-family: inherit;
      font-weight: 700;
      color: var.$clr-txt-dark;
    }

    .search-btn {
      padding: 17px 30px;
      background: transparent;
      border: none;
      cursor: pointer;

      img {
        width: 36px;
      }
    }
  }
}
</style>