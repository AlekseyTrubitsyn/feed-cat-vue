<template>
  <div @click="handleItemClick"
       @mouseleave="handleMouseLeave"
       @mouseover="handleMouseOver"
       class="catalog-item"
       v-bind:class="{ selected: selected, 'ignore-hover': ignoreHover }">
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
        <h2 class="catalog-item-main__title">Нямушка</h2>
        <h3 class="catalog-item-main__subtitle">с фуа-гра</h3>
        <p class="catalog-item-main__description"><b>10</b><span> порций</span></p>
        <p class="catalog-item-main__description">мышь в подарок</p>
      </div>
      <img class="catalog-item-main__image" src="../assets/img/cat.png" alt="Нямушка с фуа-гра" width="303" height="268">
      <p class="catalog-item-main__quantity"><span>0,5</span><span>кг</span></p>
    </div>
    <div class="catalog-item__footer ignore-click">
      <p v-show="!disabled && selected">Печень утки разварная с артишоками.</p>
      <p v-show="!disabled && !selected">Чего сидишь? Порадуй котэ, <a class="catalog-item-footer__link" href="#">купи</a><span>.</span></p>
      <p v-if="disabled">Печалька, с фуа-гра закончился.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CatalogItem",
  data() {
    return {
      itemState: 0,
      selected: false,
      ignoreHover: false,
      showHoverText: false,
      disabled: false
    };
  },
  methods: {
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
