<template>
  <div @click="handleItemClick"
       @mouseleave="handleMouseLeave"
       @mouseover="handleMouseOver"
       class="catalog-item"
       :class="{ selected: selected, 'ignore-hover': ignoreHover, disabled: item.disabled }">
    <div class="catalog-item__header">
      <div class="catalog-item-header__pre-corner ignore-click"/>
      <div class="catalog-item-header__corner"/>
      <p class="catalog-item-header__text">
        <span v-if="showHoverText">Котэ&nbsp;не&nbsp;одобряет?</span>
        <span v-else>Сказочное заморское яство</span>
      </p>
    </div>
    <div class="catalog-item__main">
      <div class="catalog-item-main__container">
        <h2 class="catalog-item-main__title">{{ item.title }}</h2>
        <h3 class="catalog-item-main__subtitle">{{ item.subtitle }}</h3>
        <p v-for="(feature, index) in item.description"
           :key="index"
           class="catalog-item-main__description"
           v-html="highlightNumbers(feature)">
           {{ feature }}
        </p>
      </div>
      <img class="catalog-item-main__image"
           :src="imagePath"
           :alt="item.image.alt"
           :width="item.image.width"
           :height="item.image.height">
      <p class="catalog-item-main__quantity"><span>{{ item.size }}</span><span>кг</span></p>
    </div>
    <div class="catalog-item__footer ignore-click">
      <p v-show="!disabled && selected">{{ item.footerDescription }}</p>
      <p v-show="!disabled && !selected">Чего сидишь? Порадуй котэ, <a class="catalog-item-footer__link" href="#">купи</a><span>.</span></p>
      <p v-if="disabled">Печалька, с {{ item.subtitle }} закончился.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CatalogItem",
  props: ["item"],
  data() {
    return {
      itemState: 0,
      selected: false,
      ignoreHover: false,
      showHoverText: false,
      disabled: this.item.disabled
    };
  },
  computed: {
    imagePath() {
      return require("@/assets/img/" + this.item.image.source);
    }
  },
  methods: {
    highlightNumbers(value) {
      return value
        .split(" ")
        .map(item => {
          if (isNaN(item)) {
            return "<span>" + item + "</span>";
          } else {
            return "<b>" + item + "</b>";
          }
        })
        .join(" ");
    },
    handleItemClick: function(e) {
      e.preventDefault();
      e.stopPropagation();

      if (this.disabled || !this.isClickable(e)) return;

      this.ignoreHover = !this.selected;
      this.selected = !this.selected;
      this.showHoverText = false;
    },
    handleMouseLeave: function() {
      this.showHoverText = false;

      if (this.ignoreHover) {
        this.itemState = 1;
        this.ignoreHover = false;
      }
    },
    handleMouseOver: function() {
      if (this.selected && !this.ignoreHover) {
        this.showHoverText = true;
      }
    },
    isClickable: function(e) {
      if (clicksDisabled(e.target)) return false;

      if (clicksDisabled(e.target.parentNode) && !(e.target.tagName === "A")) {
        return false;
      }

      return true;

      function clicksDisabled(element) {
        return element.classList.contains("ignore-click");
      }
    }
  }
};
</script>

<style lang="scss">
@import "../styles/catalog-item/catalog-item.scss";
</style>
