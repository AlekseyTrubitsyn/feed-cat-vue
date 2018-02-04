<template>
  <div id="app">
    <Header/>
    <div class="catalog">
      <CatalogItem v-for="item in items"
                   :key="item.id"
                   :item="item"/>
    </div>
  </div>
</template>

<script>
import data from "./data.json";
import Header from "./components/Header.vue";
import CatalogItem from "./components/CatalogItem.vue";

export default {
  name: "app",
  data() {
    return {
      items: data.items
    };
  },
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
