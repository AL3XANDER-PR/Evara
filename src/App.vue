<script setup>
import { onMounted, ref, watch } from "vue";

import Header from "./components/Header.vue";
import Product from "./components/Product.vue";

import { db } from "./assets/db/datos";

const carrito = ref([]);
const products = ref(db);

watch(
  carrito,
  () => {
    guardarLocalStorage();
  },
  { deep: true }
);

onMounted(() => {
  const carritoStorage = localStorage.getItem("carrito");
  if (carritoStorage) {
    carrito.value = JSON.parse(carritoStorage);
  }
});

const agregarCarrito = (product) => {
  const existeCarrito = carrito.value.findIndex(
    (producto) => producto.id === product.id
  );
  if (existeCarrito >= 0) {
    carrito.value[existeCarrito].cantidad++;
  } else {
    product.cantidad = 1;
    carrito.value.push(product);
  }
};

const eliminarProducto = (id) => {
  carrito.value = carrito.value.filter((product) => product.id !== id);
};

const guardarLocalStorage = () => {
  localStorage.setItem("carrito", JSON.stringify(carrito.value));
};
</script>

<template>
  <Header :carrito="carrito" @eliminar-producto="eliminarProducto" />
  <div class="container">
    <div class="grid-products">
      <Product
        v-for="product in products"
        :product="product"
        @agregar-carrito="agregarCarrito"
      />
    </div>
  </div>
</template>
<style scoped>
.grid-products {
  display: grid;
  grid-gap: 20px;
  grid-template-columns: repeat(auto-fill, minmax(min(100%, 18rem), 1fr));
  grid-template-rows: auto;
}
</style>
