<script setup>
const props = defineProps({
  product: {
    type: Object,
    required: true,
  },
});

defineEmits(['agregar-carrito'])
</script>

<template>
  <div class="p-3 rounded-4 card-clothing position-relative">
    <div class="position-absolute product-badges" :class="product.badges.class">
      {{ product.badges.type }}
    </div>
    <img :src="product.img" alt="" class="img-fluid rounded-4" />
    <div class="px-3 pt-3">
      <a class="product-category">Clothing</a>
      <p class="mb-0">
        <a href="#" class="product-title">{{ product.name }}</a>
      </p>
      <div class="rating-result">
        <span>
          <span>{{ product.rating }}%</span>
        </span>
      </div>

      <div class="product-price">
        <span>${{ product.precio }} </span>
        <span class="old-price">${{ product.oldPrecio }}</span>
      </div>

      <div class="product-action-1 show">
        <button
          data-bs-toggle="tooltip"
          data-bs-placement="top"
          data-bs-custom-class="custom-tooltip"
          data-bs-title="This top tooltip is themed via CSS variables."
          aria-label="Add To Cart"
          class="action-btn hover-up"
          @click="$emit('agregar-carrito',product)"
        >
          <i class="fa-regular fa-circle-plus"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-clothing {
  border: 1.5px solid #cce7d0 !important;
}

.product-badges {
  left: 25px;
  top: 25px;
  display: inline-block;
  font-size: 12px;
  line-height: 1;
  border-radius: 40px;
  color: #fff;
  padding: 5px 10px;
}

.Hot {
  background-color: #ff75a0;
}
.New {
  background-color: #99bbad;
}

.best-sell {
  background-color: #ffab73;
}
.Sale {
  background-color: #a1cae2;
}
.discount {
  background-color: #ff75a0;
}

.product-category {
  color: #90908e;
  font-size: 12px;
  text-decoration: none;
  cursor: pointer;
}

.product-title {
  font-size: 18px;
  font-family: "Spartan";
  color: #1a1a1a;
  text-decoration: none;
  cursor: pointer;
  font-weight: 500;
}

.rating-result {
  display: flex;
  align-items: center;
}
.rating-result::before {
  font-family: "fontawesome";
  font-size: 11px;
  letter-spacing: 2px;
  content: "\f005""\f005""\f005""\f005""\f005";
  color: #ffb300;
}
.rating-result > span {
  display: block;
  overflow: hidden;
  margin-left: 5px;
  font-size: 15px;
}

.product-action-1.show {
  visibility: visible;
  position: absolute;
  opacity: 1;
  bottom: 26px;
  right: 15px;
  -webkit-transform: none;
  transform: none;
  text-align: center;
}

.action-btn {
  width: 40px;
  height: 40px;
  border-radius: 50px;
  background-color: #cce7d0;
  text-align: center;
  margin-right: 3px;
  position: relative;
  display: inline-block;
  border: 1px solid #b8f0c1;

  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none;
}

.action-btn i {
  font-size: 20px;
  margin-left: 1px;
  color: #088178;
}

.product-price span {
  font-size: 20px;
  font-weight: bold;
  color: #088178;
}
.product-price span.old-price {
  font-size: 18px;
  font-weight: 400;
  color: #90908e;
  margin: 0 0 0 7px;
  text-decoration: line-through;
}
</style>
