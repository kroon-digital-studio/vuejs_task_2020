<template>
<!-- 1. Missing the main <div>. -->
  <div class="loader-wrapper" v-show="loading">
    <p>Loading...</p>
  </div>
  <div class="error-wrapper" v-show="showErrorMessage">
    <p>Something went wrong. Please try again later.</p>
  </div>
  <div class="list-wrapper" v-show="listItem.length">
    <h1 class="list-wrapper__title">List Items</h1>
    <ul class="list-wrapper__list">
      <!-- 2.1 the component is not well defined.  -->
      <!-- 2.2 not mix v-for and v-if  -->
      <!-- 2.3 var listItems should be displayed by some filtering method -->
      <list-item
        v-for="item in listItems"
        v-if="item.active"
        :key="item.id"
        item-data="item"
      />
    </ul>
  </div>
</template>

<script>
// 3. missing import components
export default {
  components: {
    ListItem
  },
  data() {
  // 4. Missing return
    listItems: [],
    showErrorMessage: false,
    loading: true
  },
  beforeCreate() {
    this.$store.dispatch("getListItems").then(function(response) {
      const { data } = response;
      this.listItems = data;
      this.loading = false;
    }).catch(function() {
      this.showErrorMessage = true;
    });
  }
}
</script>

<style>
.loader-wrapper {
  p {
    /* some css */
  }
}
.error-wrapper {
  p {
    /* some css */
  }
}
.list-wrapper {
  &__title {
    /* some css */
  }
  &__list {
    /* some css */
  }
}
</style>
