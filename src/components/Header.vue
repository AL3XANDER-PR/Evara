<script setup>
import { computed } from "vue";

const props = defineProps({
  carrito: {
    type: Object,
    required: true,
  },
});

defineEmits(['eliminar-producto'])


const totalPagar = computed(() => {
  return props.carrito.reduce(
    (total, producto) => total + producto.cantidad * producto.precio,
    0
  );
});
</script>
<template>
  <nav class="navbar navbar-expand-lg position-relative bg-white">
    <div class="container">
      <a class="navbar-brand" href="#">
        <img
          src="https://wp.alithemes.com/html/evara/evara-frontend/assets/imgs/theme/logo.svg"
          alt="logo evara"
          width="120"
          height="33"
        />
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <div class="d-flex ms-auto justify-content-between" role="search">
          <a class="icon-link"><i class="fa-regular fa-heart"></i></a>
          <a class="icon-link icon-shopping">
            <i class="fa-regular fa-bag-shopping"></i>
            <div class="shopping-car position-absolute shadow bg-white">
              <div
                v-if="carrito.length === 0"
                class="text-center d-flex align-items-center justify-content-center"
              >
                <p>Carrito Vacio</p>
              </div>
              <div v-else class="carrito">
                <table class="table">
                  <tr v-for="product in carrito">
                    <td class="px-3">
                      <div
                        class="d-flex align-items-start justify-content-around flex-row"
                        style=""
                      >
                        <img :src="product.img" alt="" width="90" />
                        <div class="d-flex flex-row">
                          <div>
                            <a
                              href=""
                              class="text-decoration-none text-primary"
                              style="font-size: 15px"
                              >{{ product.name }}</a
                            >
                            <p style="font-size: 15px">
                              {{ product.cantidad }}x{{ product.precio }}
                            </p>
                          </div>
                        </div>
                        <span @click="$emit('eliminar-producto',product.id)"><i class="fa-regular fa-trash"></i></span>
                      </div>
                    </td>
                  </tr>
                  <tr>
                    <td class="px-4 d-flex justify-content-between">
                      <div class="fs-5">Total</div>
                      <div class="fw-bolder">${{totalPagar}}</div>
                    </td>
                  </tr>
                </table>
              </div>
            </div>
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>
<style scoped>
.icon-link {
  text-decoration: none;
  margin-left: 15px;
  font-size: 20px;
  color: rgb(41, 41, 41);
}

.shopping-car {
  display: none;
  min-width: 350px;
  max-width: 350px;
  max-height: 400px;
  overflow: hidden;
  overflow-x: hidden;
  overflow-y: auto;
  z-index: 1;
  top: 40px;
  right: 310px;
}

.icon-shopping:hover > .shopping-car {
  display: block;
}
</style>
