<template>
  <div>
    <input
      v-model="searchQuery"
      @keyup.enter="searchAddress"
      placeholder="Enter a contract address"
    />
    <button @click="searchAddress">Search</button>
    <div v-if="addressData">
      <h2>Address Details</h2>
      <pre>{{ addressData }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      addressData: null,
    };
  },
  methods: {
    async searchAddress() {
      if (!this.searchQuery) {
        alert('Please enter an address.');
        return;
      }

      try {
        const response = await fetch(`https://api.sampleapis.com/beers/${this.searchQuery}`);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        this.addressData = await response.json();
      } catch (error) {
        console.error('There was a problem with the fetch operation:', error.message);
        this.addressData = null;
      }
    },
  },
};
</script>

<style>
/* Add styles if necessary */
</style>

