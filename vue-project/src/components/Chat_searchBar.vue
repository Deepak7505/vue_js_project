<template>
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-12 col-md-8">
          <form @submit.prevent="handleSubmit">
            <div class="input-group">
              <input
                type="text"
                class="form-control"
                v-model="searchQuery"
                placeholder="Search..."
              />
              <div class="input-group-append">
                <button class="btn btn-primary" type="submit">
                  Search
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        searchQuery: "",
      };
    },
    methods: {
      handleSubmit() {
        console.log("Search query:", this.searchQuery);
        // Handle the search query submission
      },
    },
  };
  </script>
  
  <style scoped>
  /* Additional styling (if needed) */
  .input-group {
    margin-top: 15px;
  }
  </style>
  