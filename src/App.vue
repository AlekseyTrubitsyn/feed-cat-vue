<template>
  <div id="app">
    <Header/>
    <div class="catalog">
      <CatalogItem/>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import CatalogItem from "./components/CatalogItem.vue";

export default {
  name: "app",
  components: {
    Header,
    CatalogItem
  }
};
</script>

<style lang="scss">
@import "./styles/media-variables";

.catalog {
  display: flex;

  width: 100%;

  flex-wrap: wrap;
  justify-content: center;
}

@media (max-width: $max-catalog-width) and (min-width: $min-tablet-width) {
  .catalog {
    justify-content: space-around;
  }
}

@media (max-width: $min-tablet-width - 1px) {
  .catalog {
    flex-direction: column;
  }
}
</style>
