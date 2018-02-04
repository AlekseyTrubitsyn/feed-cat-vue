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
import Header from "./components/Header.vue";
import CatalogItem from "./components/CatalogItem.vue";

export default {
  name: "app",
  data() {
    return {
      items: [
        {
          id: 1,
          disabled: false,
          title: "Нямушка",
          subtitle: "с фуа-гра",
          description: ["10 порций", "мышь в подарок"],
          image: {
            source: "cat.png",
            width: "303",
            height: "268",
            alt: "Нямушка с фуа-гра"
          },
          size: "0,5",
          footerDescription: "Печень утки разварная с артишоками."
        },
        {
          id: 2,
          disabled: false,
          title: "Нямушка",
          subtitle: "с рыбой",
          description: ["40 порций", "2 мыши в подарок"],
          image: {
            source: "cat.png",
            width: "303",
            height: "268",
            alt: "Нямушка с рыбой"
          },
          size: "2",
          footerDescription: "Головы щучьи с чесноком да свежайшая сёмгушка."
        },
        {
          id: 3,
          disabled: true,
          title: "Нямушка",
          subtitle: "с курой",
          description: ["100 порций", "5 мышей в подарок", "заказчик доволен"],
          image: {
            source: "cat.png",
            width: "303",
            height: "268",
            alt: "Нямушка с курой"
          },
          size: "5",
          footerDescription: "Филе из цыплят с трюфелями в бульоне."
        }
      ]
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
