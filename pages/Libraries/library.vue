<template>
  <div>
    <header class="py-8 px-4 md:px-16">
      <div class="container mx-auto flex justify-between items-center">
        <img src="../../img/LendCash_Logo-removebg-preview.png" class="w-20" alt="logo">
        <!-- <h1 class="text-3xl font-bold text-gray-800">LendCash</h1> -->
      </div>
    </header>
  </div>

  <div class="container">
    <!-- Create button aligned to the top-right -->
    <div class="header">
      <button class="bg-black text-white px-4 py-2 rounded-md hover:bg-green-900">Create</button>
    </div>

    <!-- Search bar centered under the create button -->
    <div class="search-bar">
      <input
        type="text"
        placeholder="Search..."
        v-model="searchQuery"
        @input="filterData"/>
    </div>

    <!-- Section to display filtered data with action buttons -->
    <div class="data-section">
      <div class="data-content">
        <p v-if="filteredData.length">Results for: {{ searchQuery }}</p>
        <p v-else>No matching data found.</p>
      </div>

      <!-- Buttons (View, Update, Delete) aligned to the top-right of the data section -->
      <div class="action-buttons">
        <button class="bg-black text-white px-4 py-2 rounded-md hover:bg-green-900">View</button>
        <button class="bg-black text-white px-4 py-2 rounded-md hover:bg-green-900">Update</button>
        <button class="bg-black text-white px-4 py-2 rounded-md hover:bg-green-900">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      items: [
          {  },
          {  },
          {  },
      ],
      filteredData: []
    };
  },
  mounted() {
    this.filteredData = this.items; // Initialize with all items
  },
  methods: {
    filterData() {
      this.filteredData = this.items.filter(item =>
        item.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
};




</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.header {
  display: flex;
  justify-content: flex-end; /* Align the create button to the right */
  margin-bottom: 20px;
}

.create-btn {
  padding: 10px 20px;
}

.search-bar {
  display: flex;
  justify-content: center; /* Center the search bar */
  margin-bottom: 20px;
}

.search-bar input {
  width: 300px;
  padding: 10px;
  border: 2px solid black;
}

.data-section {
  border: 1px solid #ddd;
  padding: 20px;
  position: relative;
}

.data-content {
  margin-bottom: 20px;
}

.action-buttons {
  position: absolute;
  top: 10px;
  right: 10px; /* Align buttons to the top-right */
}

.action-buttons button {
  margin-left: 10px;
  padding: 5px 10px;
}
</style>