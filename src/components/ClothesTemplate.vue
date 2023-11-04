<template>
    <v-container class="fill-height mt-16" >
      <v-responsive class="align-center text-center fill-height">
      <v-row class="ml-5 mt-2 mb-2">
      <h2>Clothes list</h2>
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
      image: "src/assets/vet/vet-1.jpg",
      price: 150,
      quantity: 1
    },

    {
      image: "src/assets/vet/vet-5.jpg",
      price: 75,
      quantity: 1
    },  {
      image: "src/assets/vet/vet-2.jpg",
      price: 100,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-1.jpg",
      price: 120,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-6.jpg",
      price: 50,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-3.jpg",
      price: 90,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-4.jpg",
      price: 70,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-7.jpg",
      price: 110,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-8.jpg",
      price: 105,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-9.jpg",
      price: 130,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-10.jpg",
      price: 170,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-11.jpg",
      price: 200,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-12.jpg",
      price: 90,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-13.jpg",
      price: 80,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-14.jpg",
      price: 56,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-15.jpg",
      price: 85,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-16.jpg",
      price: 110,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-17.jpg",
      price: 60,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-18.jpg",
      price: 140,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-19.jpg",
      price: 75,
      quantity: 1
    },
    {
      image: "src/assets/vet/vet-20.jpg",
      price: 150,
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
