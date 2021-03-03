<template>
  <button @click="getRandomQuote">get quote</button>
  <p>{{ quoteOfTheDay }}</p>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      quotes: [],
      quoteOfTheDay: "",
    };
  },
  methods: {
    async getQuotes() {
      const res = await fetch(`https://type.fit/api/quotes`);
      const quotes = await res.json();
      this.quotes = quotes;
    },
    getRandomQuote() {
      const index = Math.floor(Math.random() * this.quotes.length);
      const quoteOfTheDay = this.quotes[index];
      this.quoteOfTheDay = quoteOfTheDay.text;
    },
  },
  async beforeMount() {
    await this.getQuotes();
    this.getRandomQuote();
  },
};
</script>