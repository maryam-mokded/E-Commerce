<template>
    <v-container class="fill-height mt-16" >
      <v-responsive class="align-center text-center fill-height">
      <v-row class="ml-5 mt-2 mb-2">
        <h2>Electronics element list</h2>
      </v-row>
        <v-row>
          <v-col v-for="item in items">
            <v-card class="mx-auto" max-width="200">
              <v-img
                :width="200"
                :height="150"
                aspect-ratio="16/9"
                cover
                :src="item.image"
              ></v-img>

              <v-card-title> price : {{ item.price }} </v-card-title>

              <v-card-actions>
                  <v-row align="center" justify="center">
                    <v-btn  color="#08AC0C" variant="flat" prepend-icon="mdi-plus-thick" @click="AddToCart(item)"> Add to cart </v-btn>
                  </v-row>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-responsive>
    </v-container>
  </template>

  <script lang="ts" setup>
  import { ref } from "vue";
  const items = ref([
    {
      image: "src/assets/Elect/elec-1.jpg",
      price: 150,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-5.jpg",
      price: 75,
      quantity: 1
    },  {
      image: "src/assets/Elect/elec-2.jpg",
      price: 100,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-1.jpg",
      price: 120,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-6.jpg",
      price: 50,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-3.jpg",
      price: 90,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-4.jpg",
      price: 70,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-7.jpg",
      price: 110,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-8.jpg",
      price: 105,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-9.jpg",
      price: 130,
      quantity: 1
    },
    {
      image: "src/assets/Elect/elec-10.jpg",
      price: 170,
      quantity: 1
    },
  ]);

  const shopping_cart = ref([])
  function AddToCart(item: any){
    const selected_element = JSON.parse(JSON.stringify(item))
    shopping_cart.value = JSON.parse(localStorage.getItem('cart') || 'null')
    console.log(shopping_cart.value);
    if(shopping_cart.value == null){
        shopping_cart.value = []
        shopping_cart.value.push(selected_element)
    }else{
        shopping_cart.value.push(selected_element)
    }
    localStorage.setItem('cart', JSON.stringify(shopping_cart.value))
    // localStorage.setItem('cart', JSON.stringify(selected_element))
  }
  </script>
