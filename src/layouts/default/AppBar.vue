<template>
  <v-app-bar flat>
    <v-app-bar-title  class="font-weight-black">
      <v-icon icon="mdi-cart-minus" color="#08AC0C" />
      FreshCart
    </v-app-bar-title>
    <v-btn color="#08AC0C" to="/shoppingCart">
      <v-badge color="error" dot v-if="totale_shopping_cart != null">
        <v-icon
          icon="mdi-shopping-outline"
          color="#08AC0C"
          size="large"
          start
        />
      </v-badge>
      <v-icon
      v-else
          icon="mdi-shopping-outline"
          color="#08AC0C"
          size="large"
          start
        />
    </v-btn>
  </v-app-bar>
  <v-app-bar height="18px">
    <v-btn color="#08AC0C" prepend-icon="mdi-home-outline" to="/home">Home</v-btn>

    <v-menu>
      <template v-slot:activator="{ props }">
        <v-btn v-bind="props" color="#08AC0C" prepend-icon="mdi-rhombus-split"  append-icon="mdi-menu-down">Collections</v-btn>
      </template>
      <v-list>
        <v-list-item  to="/clothes">
          <v-list-item-title>Clothes</v-list-item-title>
        </v-list-item>
        <v-list-item  to="/accessories">
          <v-list-item-title>Accessoires</v-list-item-title>
        </v-list-item>
        <v-list-item  to="/electronics">
          <v-list-item-title>Electronics</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    <v-btn color="#08AC0C" prepend-icon="mdi-account-outline" to="account">Account </v-btn>
    <v-btn color="#08AC0C" prepend-icon="mdi-card-account-mail-outline" to="/contact">Contact</v-btn>
  </v-app-bar>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
const totale_shopping_cart = ref(null)
if( JSON.parse(localStorage.getItem("cart") || "null") != null){
  totale_shopping_cart.value = JSON.parse(localStorage.getItem("cart") || "null").length;
}

</script>
